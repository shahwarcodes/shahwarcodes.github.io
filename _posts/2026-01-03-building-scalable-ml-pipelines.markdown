---
layout: post
title: "Building Scalable ML Pipelines: Lessons from Production"
date: 2026-01-03 10:00:00
excerpt: "Key insights from building ML pipelines that process 30TB of data daily, including architecture decisions, common pitfalls, and practical tips for scaling ML infrastructure."
mathjax: true
---

Over the past few years, I've built ML pipelines that process massive amounts of data in production. Here are some key lessons I've learned about building systems that scale.

## The Architecture Challenge

When you're processing 30TB of data daily, traditional batch processing approaches quickly show their limitations. The key insight is to design your pipeline as a directed acyclic graph (DAG) of independent, composable steps.

### Config-Driven Design

One of the best decisions we made was adopting a config-driven architecture. Instead of hard-coding pipeline logic, we define workflows in YAML:

```python
from dataclasses import dataclass
from typing import List, Dict, Any

@dataclass
class PipelineConfig:
    name: str
    steps: List[Dict[str, Any]]
    resources: Dict[str, int]

    def validate(self) -> bool:
        # Validate DAG structure
        return all(self._validate_step(s) for s in self.steps)
```

This approach has several advantages:

1. **Reproducibility**: Configs are versioned alongside code
2. **Flexibility**: Easy to modify without code changes
3. **Testing**: Can validate configs independently

## The Math Behind Optimization

When optimizing data processing, understanding the theoretical limits helps. For a pipeline with \\(n\\) stages, the total processing time \\(T\\) is:

$$T = \sum_{i=1}^{n} t_i + \sum_{i=1}^{n-1} d_i$$

where \\(t_i\\) is the processing time for stage \\(i\\) and \\(d_i\\) is the data transfer delay between stages.

The key to optimization is minimizing both computation time and data movement. In practice, data transfer often dominates:

$$d_i \gg t_i$$

This means **collocating compute and storage** is crucial for performance.

## Practical Tips

### 1. Embrace Idempotency

Every pipeline step should be idempotent. This makes retries safe and debugging easier:

```python
def process_batch(batch_id: str, input_path: str, output_path: str):
    # Check if already processed
    if output_exists(output_path):
        logger.info(f"Batch {batch_id} already processed")
        return

    # Process data
    data = load_data(input_path)
    result = transform(data)

    # Atomic write
    write_atomic(result, output_path)
```

### 2. Monitor Everything

Use metrics to understand your pipeline's behavior:

```python
from prometheus_client import Counter, Histogram

batch_processed = Counter('batches_processed_total', 'Total batches processed')
processing_time = Histogram('batch_processing_seconds', 'Time to process batch')

@processing_time.time()
def process_batch(batch):
    # Processing logic
    batch_processed.inc()
```

### 3. Handle Failures Gracefully

In distributed systems, failures are inevitable. Design for them:

```python
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential(multiplier=1, min=4, max=10)
)
def fetch_data(url: str) -> bytes:
    response = requests.get(url, timeout=30)
    response.raise_for_status()
    return response.content
```

## Workflow Orchestration

We use [Flyte](https://flyte.org) for orchestration. It provides:

- **Versioning**: Track pipeline versions over time
- **Caching**: Reuse results from previous runs
- **Observability**: Built-in metrics and logging

Here's a simple Flyte workflow:

```python
from flytekit import task, workflow

@task
def load_data(path: str) -> pd.DataFrame:
    return pd.read_parquet(path)

@task
def transform_data(df: pd.DataFrame) -> pd.DataFrame:
    return df.groupby('user_id').agg({'value': 'sum'})

@workflow
def ml_pipeline(input_path: str) -> pd.DataFrame:
    data = load_data(path=input_path)
    return transform_data(df=data)
```

## Key Takeaways

1. **Design for scale from the start** - Retrofitting is painful
2. **Make pipelines config-driven** - Flexibility pays dividends
3. **Embrace functional patterns** - Immutability and pure functions reduce bugs
4. **Monitor relentlessly** - You can't fix what you can't measure
5. **Plan for failure** - Retries, timeouts, and circuit breakers are essential

Building scalable ML infrastructure is challenging, but following these principles has helped us maintain reliable systems processing terabytes of data daily.

---

*What challenges have you faced scaling ML pipelines? I'd love to hear your experiences.*
