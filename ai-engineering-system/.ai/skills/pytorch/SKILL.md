---
name: pytorch
description: Develop and review PyTorch model code. Use when implementing neural networks, datasets, dataloaders, training loops, evaluation, checkpointing, or computer vision experiments.
---

# PyTorch

## Purpose

Keep PyTorch experiments correct, reproducible, and easy to evaluate.

## When to use

Use this skill for model architecture, training loops, GPU behavior, tensor shapes, losses, metrics, and experiment debugging.

## Decision rules

- Make tensor shapes explicit in comments or assertions when risk is high.
- Separate dataset, model, training, evaluation, and configuration.
- Control randomness for reproducible comparisons.
- Save checkpoints with enough metadata to resume or audit.
- Evaluate with metrics aligned to the research or product goal.

## Anti-patterns

- Mixing preprocessing, model definition, and training control in one script.
- Comparing experiments without fixed seeds or tracked configs.
- Ignoring device placement and dtype assumptions.
- Reporting only training loss.

## Checklist

- Verify input and output shapes.
- Check dataset and transform assumptions.
- Track hyperparameters and seeds.
- Validate train/eval mode transitions.
- Save metrics, checkpoints, and configuration.
