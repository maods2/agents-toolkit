---
name: mlops
description: Design and operate machine learning workflows. Use when working with data pipelines, model training, evaluation, deployment, monitoring, reproducibility, or experiment governance.
---

# MLOps

## Purpose

Make ML systems reproducible, observable, and safe to operate across data, training, evaluation, and deployment stages.

## When to use

Use this skill for ML pipelines, model lifecycle work, data validation, experiment tracking, deployment readiness, or production monitoring.

## Decision rules

- Track data, code, parameters, metrics, and artifacts together.
- Separate training, evaluation, and inference concerns.
- Validate data before training and serving.
- Define promotion criteria before deployment.
- Monitor model and data behavior after release.

## Anti-patterns

- Optimizing offline metrics without deployment constraints.
- Treating notebooks as production pipelines.
- Ignoring data drift and label quality.
- Deploying without rollback or monitoring plans.

## Checklist

- Define pipeline stages.
- Record inputs, outputs, and artifacts.
- Specify metrics and acceptance thresholds.
- Check reproducibility.
- Plan deployment, monitoring, and rollback.
