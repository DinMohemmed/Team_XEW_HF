# GitPulse Gemma — Open-Source Contribution Finder

> **Hacktoberfest Hack Day Submission**
> - **Problem Statement**: **#20 — Open-Source Contribution Finder**
> - **Track**: **Track 2: Best Use of Gemma**
> - **AI Model**: **Google Gemma (`gemma2:2b` via Local Ollama)**
> - **License**: [MIT License](./LICENSE) + [Gemma Terms of Use](https://ai.google.dev/gemma/terms)

---

## 🎯 The Problem We Solve
First-time open-source contributors and 1st-year university students face three major roadblocks during Hacktoberfest:
1. **Ghost & Taken Issues**: Spending hours reading an issue only to discover someone else is already assigned (`assignee != null`) or the issue has been stale for months.
2. **Intimidating Developer Jargon**: Maintainers write terse issue descriptions filled with internal stack trace jargon that overwhelms beginners.
3. **Cold-Start Paralysis**: Not knowing which terminal commands to run or which files to inspect first.

**GitPulse Gemma** solves all three by combining a **Real-Time "Actually Open" Readiness Filter** with **Google's `gemma2:2b` running locally on Ollama**.

---

## 🏗️ System Architecture

```mermaid
flowchart LR
    A[User Selects Stack & Experience Level] --> B[Flask Backend :5002]
    B -->|Live REST Search| C[GitHub Issues API]
    B -->|Zero-Fail Demo Mode| D[Curated Live Dataset]
    C --> E[Real-Time 'Actually Open' Filter]
    D --> E
    E -->|Drops Assigned, Closed & Stale Issues| F[Verified Unassigned Issues]
    F -->|Structured JSON Prompt| G[Local Ollama: gemma2:2b]
    G -->|Returns match_score, why_it_fits, jargon_buster, first_3_steps| H[Light-Mode Bento UI + PR Starter Modal]
