---
title: "Day 1: AI Platform Engineering Architecture Layers"
date: 2026-11-09
draft: false
tags: ["aipe", "architecture", "platform-engineering"]
---

## What it is
An AI **application** is a prompt plus a model. An AI **platform** is everything that keeps many such applications fast, safe, cheap and observable. Layer counts differ between vendors (three to six in the sources I checked), so this is my working model, not a standard.

| # | Layer | Examples |
|---|---|---|
| 1 | Apps and agents | chatbots, copilots, SRE agents |
| 2 | Orchestration | workflows, tools, memory, LangGraph |
| 3 | Model gateway | routing, retries, fallbacks |
| 4 | Data and retrieval | RAG, vector DB |
| 5 | Runtime | Docker, Kubernetes, FastAPI |
| 6 | Cloud and IaC | AWS, Terraform |
| X | Cross-cutting | security, observability, CI/CD, cost |

## Why it matters for an AI Platform Engineer
Production failures happen at layer boundaries. Knowing the layers tells you where to look first.

## Hands-on lab
Code: `aipe-labs/day-001-aipe-architecture-layers`. Run `python layers.py`, then `FAIL_LAYER=retrieval python layers.py`.

## Break / Fix
Injected failure in the retrieval layer. The log shows `request failed: retrieval layer failed` and the trace ends after `gateway`. Fix: remove the injected variable. Lesson: per-layer logging turns "it is broken" into "this layer is broken".

## Interview question
*What is AIPE architecture layers, and where does it sit?* Answer: an AI platform is a stack of layers (apps, orchestration, model gateway, data, runtime, cloud) with security, observability, CI/CD and cost cutting across all of them. The platform engineer owns the shared layers so product teams ship AI features without rebuilding them.

## Further reading
- [Building effective agents - Anthropic](https://www.anthropic.com/engineering/building-effective-agents)
- [awesome-platform-engineering](https://github.com/shospodarets/awesome-platform-engineering)
- [NVIDIA GenerativeAIExamples](https://github.com/NVIDIA/GenerativeAIExamples)

