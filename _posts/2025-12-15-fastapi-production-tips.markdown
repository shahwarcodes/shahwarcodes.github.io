---
layout: post
title: "FastAPI in Production: 5 Things I Wish I Knew Earlier"
date: 2025-12-15 14:30:00
excerpt: "Practical lessons from running FastAPI services at scale, including performance optimization, testing strategies, and common pitfalls to avoid."
---

After running FastAPI services handling millions of requests daily, here are five things I wish I'd known from the start.

## 1. Use Dependency Injection Properly

FastAPI's dependency injection is powerful, but it's easy to misuse. Here's a common mistake:

```python
# Bad: Creating new connection every request
@app.get("/users/{user_id}")
async def get_user(user_id: int):
    db = Database()  # New connection!
    return await db.get_user(user_id)

# Good: Reuse connection pool via dependency
async def get_db():
    async with db_pool.connection() as conn:
        yield conn

@app.get("/users/{user_id}")
async def get_user(user_id: int, db=Depends(get_db)):
    return await db.get_user(user_id)
```

## 2. Async Doesn't Mean Fast

Don't blindly make everything `async`. CPU-bound operations should run in thread pools:

```python
from concurrent.futures import ThreadPoolExecutor

executor = ThreadPoolExecutor(max_workers=4)

@app.post("/process")
async def process_data(data: bytes):
    # CPU-intensive work in thread pool
    result = await asyncio.get_event_loop().run_in_executor(
        executor, expensive_computation, data
    )
    return result
```

## 3. Validate Early, Validate Often

Pydantic models are great, but add custom validation for business logic:

```python
from pydantic import BaseModel, validator

class CreateUserRequest(BaseModel):
    email: str
    age: int

    @validator('email')
    def email_must_be_corporate(cls, v):
        if not v.endswith('@company.com'):
            raise ValueError('must be corporate email')
        return v

    @validator('age')
    def age_must_be_reasonable(cls, v):
        if not 18 <= v <= 120:
            raise ValueError('invalid age')
        return v
```

## 4. Structure Your Responses

Use response models to control what gets returned:

```python
class UserResponse(BaseModel):
    id: int
    email: str
    # Don't expose password_hash!

@app.get("/users/{user_id}", response_model=UserResponse)
async def get_user(user_id: int):
    user = await db.get_user(user_id)  # Has password_hash
    return user  # FastAPI filters to response_model fields
```

## 5. Monitor Your Endpoints

Add middleware to track performance:

```python
import time
from starlette.middleware.base import BaseHTTPMiddleware

class TimingMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        start = time.time()
        response = await call_next(request)
        duration = time.time() - start

        # Log slow requests
        if duration > 1.0:
            logger.warning(f"Slow request: {request.url.path} took {duration:.2f}s")

        return response

app.add_middleware(TimingMiddleware)
```

## Bonus: Testing Tips

Use `TestClient` with proper fixtures:

```python
from fastapi.testclient import TestClient
import pytest

@pytest.fixture
def client():
    return TestClient(app)

def test_create_user(client):
    response = client.post("/users", json={
        "email": "test@company.com",
        "age": 25
    })
    assert response.status_code == 201
    assert response.json()["email"] == "test@company.com"
```

---

FastAPI is a great framework, but like any tool, it requires understanding to use effectively. These patterns have saved me countless debugging hours.
