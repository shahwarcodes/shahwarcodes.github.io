---
layout: page
title: Resume
---

## Senior AI Engineer · LLM Systems & ML Platform

Toronto, ON · Canadian Citizen, US TN Visa eligible
[saleemshahwar@gmail.com](mailto:saleemshahwar@gmail.com) · [LinkedIn](https://linkedin.com/in/shahwar-saleem) · [GitHub](https://github.com/shahwarcodes)

## Summary

Senior engineer with 10+ years building ML platforms, applied AI systems, and backend infrastructure at scale. Sole engineer on an LLM-as-judge evaluation platform taken from 0 to 1 — full frontend and backend, architecture through production — now the core quality-measurement product for AI-generated legal documents at EvenUp, evaluating 600–800 documents/week and driving a weekly SME-reviewed quality-improvement loop adopted org-wide. Prior platform work spans config-driven data infrastructure at 30 TB/day, workflow orchestration on Kubernetes, secure inference gateways, and Spark-based ETL adopted across 20+ teams. Strong systems orientation across full-stack product ownership, Python backends, distributed compute, and cloud-native infrastructure (AWS, Kubernetes).

## Experience

**Senior AI Engineer, Document Generation Platform — EvenUp** *(Aug 2025 – Present)*

- Conceived, architected, and solely built an LLM-as-judge evaluation platform from 0 to 1 — full product ownership of scope, system design, backend services, and frontend UI — establishing EvenUp's first systematic quality-measurement layer for AI-generated legal documents, with zero prior tooling to build on.
- Designed the evaluation methodology and scoring rubrics across three quality pillars — writing quality, factual correctness, and formatting fidelity — and engineered three complementary run modes (on-demand manual runs, sampled auto-runs against live production traffic, and scheduled weekly runs over curated benchmark datasets) to evaluate 600–800 documents per week.
- Built the full stack as a single-owner engineer: backend evaluation orchestration and LLM-judge pipelines, scoring persistence and reporting APIs, and a frontend for run configuration, results dashboards, and defect drill-down — taking the platform from prototype to a production system used daily across the org.
- Drove business adoption by embedding the platform into a weekly SME-in-the-loop review cycle: eval reports surface systematic defects that subject-matter experts annotate, closing the loop between automated scoring and human judgment and making the platform the org's operating cadence for document-quality management.
- Used eval-platform findings to prioritize and lead the rollout of DOCX-grade formatting capabilities (indentation, margin controls, table styles, full header/footer support) comparable to Microsoft Word, directly raising the document-quality bar for Case Companion's enterprise customers.
- Leveraged the evaluation platform as the safety net for coordinating pipeline changes across 200K+ production documents, ensuring backward compatibility and zero data loss through deterministic rendering and migration validation.

**Senior MLOps Engineer, ML & Data Infrastructure — Ripple** *(Nov 2022 – Apr 2025)*

- Architected MLegobricks, a unified ML-engineering monorepo with automated packaging, CI/CD templates, semantic versioning, and one-click publishing — adopted by 12 teams, eliminating duplicated infra code and standardizing the ML release process across the org.
- Automated ML-platform migration from GCP to AWS Databricks via config-driven Python tooling and infra abstractions, collapsing a 3–4 month per-team migration into hours of work.
- Designed a secure inference gateway (OAuth2, JWT, Envoy) with RBAC and standardized service contracts, enabling safe, observable model serving across internal teams.
- Owned platform reliability and developer ergonomics; built tooling and abstractions that became the default path for ML teams shipping to production.

**Software Engineer II, ML Platform — Arctic Wolf** *(Jan 2022 – Nov 2022)*

- Led evaluation and rollout of Flyte as Arctic Wolf's unified workflow orchestrator, establishing configuration-only ML pipeline definitions and autoscaling execution semantics.
- Delivered the company's first AWS EKS-based Flyte deployment with upstream contributions, cutting per-team onboarding from weeks to 1–2 days.

**Software Engineer, Machine Learning & Data Platform — Borealis AI (RBC)** *(Jul 2019 – Jan 2022)*

- Built Anahit, a config-driven ML data platform that let researchers ingest, transform, and publish datasets using declarative YAML DSLs — eliminating bespoke ETL code and standardizing data workflows for 20+ teams.
- Designed a modular Spark-based ETL engine with pluggable source/sink connectors (S3, Teradata, NFS) processing 30 TB+ of data per day, supporting large-scale batch pipelines and high-volume model-training workloads.
- Delivered schema enforcement, partitioning, and Delta Lake optimizations (Z-ordering, indexing, storage tuning) that reduced large time-series query latency from seconds to milliseconds.
- Abstracted cluster configuration, autoscaling, and job scheduling behind declarative configs, cutting dataset onboarding time from weeks to hours for ML researchers.

**Machine Learning Engineer — ProNavigator** *(Aug 2018 – Jul 2019)*

- Achieved 100× inference speedup and 100× model-size reduction, materially cutting infrastructure cost while improving end-user latency.
- Improved production classification accuracy from 95% to 97% with seamless rollout to live insurance-intelligence workloads.
- Lifted intent-labelling accuracy from 79% to 90% by shipping a confusion-matrix tooling layer that gave data labellers actionable feedback loops.

**Software Engineer, Embedded Systems — Mentor Graphics (Siemens EDA)** *(Oct 2013 – Apr 2016)*

- Shipped Kernel Awareness for Nucleus RTOS — a feature visualizing per-process state, memory utilization, and core affinity on multi-core ARM and PPC targets.
- Developed device drivers (I2C, SPI, LCD, CAN) for embedded ARM and PPC architectures.

## Skills

**LLM & Applied AI:** LLM-as-judge evaluation, 0-to-1 eval platform design (full-stack), eval harness & scoring-rubric design, factuality & quality scoring frameworks, sampled live-traffic evaluation, SME-in-the-loop annotation workflows, eval-driven product development.

**Languages:** Python (expert), SQL, TypeScript, Bash, Go (working), C/C++ (prior).

**Backend & Distributed Systems:** FastAPI, REST/gRPC, OAuth2/JWT, Envoy, service-mesh patterns, event-driven design, large-scale system design.

**Data & ML Infra:** Apache Spark, Delta Lake, Databricks, Flyte, Airflow, MLflow, feature pipelines, schema enforcement, batch + streaming ETL.

**Cloud & Platform:** AWS (EKS, S3, IAM, EC2), GCP, Kubernetes, Docker, Terraform, CloudFormation, GitHub Actions CI/CD.

**Datastores:** PostgreSQL, S3-backed lakes, vector databases.

## Education

**M.Eng., Computer Science** — University of Waterloo *(2016 – 2018)*
Graduate Research Assistant, Autonomous Vehicles Lab. Built the ROS-on-QNX build system for in-vehicle ARM deployment; coursework in machine learning, optimization, and software architecture.

**B.Sc., Electrical & Computer Engineering** — University of Engineering & Technology, Lahore *(2009 – 2013)*

## Publication

**An Automated Vehicle Safety Concept Based on Runtime Restriction of the Operational Design Domain.** *IEEE Intelligent Vehicle Symposium, 2018.* Camera-obstruction detection for autonomous vehicles using deep neural networks integrated with ROS.
