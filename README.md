<div align="center">
  <img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white" alt="GitHub Actions" />
  <img src="https://img.shields.io/badge/CI%2FCD-Automated-4CAF50?style=for-the-badge" alt="CI/CD Automation" />
  <img src="https://img.shields.io/badge/YAML-CRON-FF1493?style=for-the-badge&logo=yaml" alt="YAML" />
  <img src="https://img.shields.io/badge/Serverless-Orchestration-000000?style=for-the-badge" alt="Serverless" />
  
  <br />
  <br />
  <h2>⚙️ Workflow Automation Engine</h2>
  <p><b>Serverless CI/CD Pipeline & Cron-Based Orchestration</b></p>
  <p><i>(Originally developed for the Tools in Data Science course at IIT Madras)</i></p>
</div>

<br />

This repository contains a streamlined, headless **GitHub Actions** orchestration pipeline. Built to execute entirely in the cloud without manual intervention, it demonstrates core **DevOps and CI/CD competencies** by automating version control operations via CRON scheduling.

While simple in its current implementation, this repository serves as a foundational blueprint for automated systems—a critical skill for AI/GenAI Engineering, where automated model retraining, nightly builds, and scheduled data ingestion pipelines are paramount.

---

## 🌟 Technical Highlights

### 1. Serverless CRON Orchestration
- Utilizes GitHub Actions' `schedule` event to trigger workflows autonomously at midnight (`0 0 * * *`) UTC.
- Completely serverless execution leveraging `ubuntu-latest` runners, requiring zero local infrastructure.

### 2. Headless Version Control (GitOps)
- Programmatically configures Git identity (`user.name`, `user.email`) within the ephemeral runner environment.
- Safely modifies state, stages artifacts, and pushes commits (`Automation by Ghazi-R3`) back to the origin using securely injected environment tokens (`GH_TOKEN`).

### 3. Modular CI/CD Extensibility
- Includes `workflow_dispatch`, allowing on-demand manual triggers of the pipeline outside of the scheduled CRON windows.
- The pipeline (`daily_commit.yml`) is structured immutably in YAML, making it easily extensible for more complex operations (e.g., triggering LLM batch inferences, scraping daily datasets, or running end-to-end tests).

---

## 🏗️ Pipeline Architecture

```mermaid
graph TD;
    subgraph GitHub Infrastructure
        A(("🕒 CRON Scheduler (Midnight)")) -->|Triggers| B["GitHub Actions Runner (Ubuntu)"];
        M(("👤 Manual Dispatch")) -->|Triggers| B;
    end
    
    subgraph Ephemeral Build Environment
        B -->|Checkout| C["Clone Repository"];
        C -->|Config| D["Inject Git Identity"];
        D -->|Execute| E["Append Timestamp to Log"];
        E -->|GitOps| F["Stage, Commit & Push"];
    end
    
    F -->|Secure Push| G[("Remote Repository")];
```

---

## 🚀 Usage & Deployment

### 1. Setup
To use this automation framework in your own repository:
1. Fork or clone this repository.
2. Ensure you have a GitHub Personal Access Token (PAT) with `repo` scopes.
3. Add the token to your repository secrets as `GH_TOKEN`.

### 2. Configuration
Modify `.github/workflows/daily_commit.yml` to adjust the CRON schedule or extend the bash execution block with custom scripts (e.g., Python scraping scripts, model evaluation runs).

---

## 💼 Why This Matters (For Tech Leadership)

As an AI/GenAI Engineer, the ability to build and deploy ML models is only half the equation. The other half is **MLOps and CI/CD**. 

This repository demonstrates the ability to step outside of Jupyter notebooks and interact with production engineering tools. Understanding how to orchestrate automated, scheduled tasks in CI/CD environments is directly transferable to building resilient AI pipelines, continuous model evaluation loops, and automated deployment architectures.
