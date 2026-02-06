# The Task

![status badge](https://github.com/PreciousDipe/Sycamore_DevOps_Assessment/actions/workflows/main.yaml/badge.svg)

## DevOps Troubleshooting Assessment

### Task Overview

1. **Deploy** the provided `broken-manifest.yaml` to a local Kubernetes cluster (Minikube or Kind).
2. **Diagnose** why the pod enters a `CrashLoopBackOff` state.
3. **Root Cause Analysis (RCA):**
	- Provide a Markdown document explaining your findings.
4. **Submit a Fixed Manifest:**
	- Ensure the service remains stable after your fix.

---

## Candidate Submission Guide

- **Format:** Link to a public GitHub repository.
- **Access:** Add the hiring lead (as specified in the email) as a collaborator.
- **Evidence:**
  - The repository must show a **Failed** run (where security caught a vulnerability).
  - The repository must show a **Successful** run (after potentially updating the base image or ignoring non-fixed vulnerabilities if allowed).

## Solution
## 🏗️ Architectural Decisions

### Task A: DevOps Troubleshooting (The 502 Mystery)

| Decision | Rationale |
|----------|-----------|
| **Application** | Memory Leak	Capped array size and trimmed it once the limit was reached to prevent memory overuse and ensure proper memory release. |
| **Resource Limits** | Increased memory request to 256Mi and memory limit to 1Gi to match application’s needs and avoid pod termination due to memory exhaustion leading to OOMKILLED error. |

### Task B: Secure CI/CD Pipeline


| Decision | Rationale |
|----------|-----------|
| **Permissions** | Grants permissions for pushing Docker images to GHCR (`write`) and reading repository contents to build the Docker image (`read`) |
| **GitHub Container Registry (GHCR)** | Authenticates to GitHub Container Registry (GHCR) using the `GITHUB_TOKEN` stored in GitHub secrets, ensuring secure access to GHCR |
| **Trivy Scan Step** |  Runs Trivy (a vulnerability scanner) on the Docker image to detect vulnerabilities. If any vulnerabilities of `HIGH` or `CRITICAL` severity are found, the build fails.|
| **Push Docker Image** | Pushes the Docker image to GitHub Container Registry (GHCR) after the image has been successfully built and scanned |
