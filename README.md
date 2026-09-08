# Nafees Ur Rehman
### AWS DevOps & Cloud Infrastructure Engineer

`nafees@platform:~$ cat engineering-focus.txt`

Building production-oriented AWS infrastructure with Terraform, Kubernetes, and reviewed delivery workflows. My portfolio connects infrastructure provisioning, CI/CD, GitOps, and Python/Bash automation with least-privilege access and reproducible operations. The repositories distinguish implemented code from cloud deployment evidence.

![Infrastructure command examples](https://readme-typing-svg.demolab.com?font=Fira+Code&size=14&duration=4200&pause=1800&color=3FB950&background=0D1117&vCenter=true&width=900&height=42&lines=aws%20sts%20get-caller-identity%20--query%20%27Account%27%20--output%20text;terraform%20plan%20-out%3Dproduction.tfplan;terraform%20apply%20production.tfplan;kubectl%20rollout%20status%20deployment%2Fcore-api%20-n%20production;trivy%20image%20--severity%20HIGH%2CCRITICAL%20backend-app%3Av1.4;argocd%20app%20sync%20production-platform)

*Illustrative commands, not a live terminal or deployment history.*

## Engineering principles

| Area | Principle |
| --- | --- |
| Infrastructure | Declarative, modular, versioned |
| Deployments | Automated, immutable, verified |
| Security | Least privilege and short-lived credentials |
| Changes | Reviewed and traceable |
| Environments | Separate state and configuration |
| Operations | Observable behavior and actionable runbooks |
| Recovery | Designed and tested before claiming readiness |

## Platform workflow

**Architect → Provision → Build → Test → Scan → Deploy → Observe → Operate**

```mermaid
flowchart TD
    PR["Reviewed source change"] --> CI["GitHub Actions: tests and validation"]
    CI --> IaC["Terraform plan / reviewed apply"]
    IaC --> AWS["VPC / IAM / private EKS workers"]
    CI --> Build["Multi-stage Docker build"]
    Build --> Scan["Trivy vulnerability gate"]
    Scan --> Registry["ECR: immutable digest"]
    Registry --> GitOps["Reviewed deployment-state pull request"]
    GitOps --> Argo["Argo CD / Helm rendering"]
    Argo --> Workload["Kubernetes application"]
    AWS --> Workload
    TLS["Ingress / cert-manager"] --> Workload
    Workload --> Ops["Health checks / logs / rollout verification"]
    Ops -.-> Planned["Planned: Prometheus / Grafana / CloudWatch workload collection"]
```

Terraform owns the cloud foundation and platform add-ons. Argo CD owns application deployment state. Planned observability integrations are shown explicitly.

## Technology focus

| Domain | Technologies |
| --- | --- |
| Cloud & IaC | ![AWS](https://img.shields.io/badge/AWS-30363d?style=flat-square) ![Amazon VPC](https://img.shields.io/badge/Amazon%20VPC-30363d?style=flat-square) ![IAM](https://img.shields.io/badge/IAM-30363d?style=flat-square) ![Amazon EC2](https://img.shields.io/badge/Amazon%20EC2-30363d?style=flat-square) ![Amazon EKS](https://img.shields.io/badge/Amazon%20EKS-30363d?style=flat-square) ![Amazon S3](https://img.shields.io/badge/Amazon%20S3-30363d?style=flat-square) ![Amazon RDS](https://img.shields.io/badge/Amazon%20RDS-30363d?style=flat-square) ![Terraform](https://img.shields.io/badge/Terraform-30363d?style=flat-square) ![OpenTofu](https://img.shields.io/badge/OpenTofu-30363d?style=flat-square) ![Linux](https://img.shields.io/badge/Linux-30363d?style=flat-square) |
| Containers & orchestration | ![Docker](https://img.shields.io/badge/Docker-30363d?style=flat-square) ![Kubernetes](https://img.shields.io/badge/Kubernetes-30363d?style=flat-square) ![Helm](https://img.shields.io/badge/Helm-30363d?style=flat-square) ![Argo CD](https://img.shields.io/badge/Argo%20CD-30363d?style=flat-square) |
| CI/CD & DevSecOps | ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-30363d?style=flat-square) ![Trivy](https://img.shields.io/badge/Trivy-30363d?style=flat-square) ![SonarQube](https://img.shields.io/badge/SonarQube-30363d?style=flat-square) ![Bash](https://img.shields.io/badge/Bash-30363d?style=flat-square) |
| Automation & integration | ![Python](https://img.shields.io/badge/Python-30363d?style=flat-square) ![REST APIs](https://img.shields.io/badge/REST%20APIs-30363d?style=flat-square) ![n8n](https://img.shields.io/badge/n8n-30363d?style=flat-square) |
| Observability | ![Prometheus](https://img.shields.io/badge/Prometheus-30363d?style=flat-square) ![Grafana](https://img.shields.io/badge/Grafana-30363d?style=flat-square) ![Amazon CloudWatch](https://img.shields.io/badge/Amazon%20CloudWatch-30363d?style=flat-square) |

The matrix describes engineering focus; it is not a claim of production experience with every technology.

## Featured engineering projects

### Modular AWS EKS platform

[Repository](https://github.com/expertnafees-hub/aws-eks-terraform-platform)

| Dimension | Implementation and intent |
| --- | --- |
| Problem | Reproduce Kubernetes infrastructure with explicit environment boundaries. |
| Architecture | Multi-AZ VPC, private managed nodes, private EKS API, IAM/IRSA, and Helm platform add-ons. |
| Decisions | Separate foundation/add-on states; reusable VPC, IAM, security, EKS, and add-on modules. |
| Security | Restricted API CIDRs, scoped controller identities, encrypted/versioned state bootstrap, and certificate automation. |
| Automation | Terraform formatting/schema checks and IaC scanning workflow. |
| Reliability | Two-node baseline, controlled node updates, separate state, and documented teardown/recovery. |
| Stack | AWS, Terraform, EKS, Helm, Traefik, cert-manager. |
| Status | Infrastructure code implemented; AWS provisioning and operational validation pending. |

Related baseline: [AWS VPC Foundation](https://github.com/expertnafees-hub/aws-terraform-vpc-foundation), a deliberately small public-subnet networking project.

### GitOps application delivery

[Application and CI](https://github.com/expertnafees-hub/gitops-core-api) · [Deployment configuration](https://github.com/expertnafees-hub/gitops-platform-config)

| Dimension | Implementation and intent |
| --- | --- |
| Problem | Trace a reviewed source change to an immutable Kubernetes release. |
| Architecture | Flask/Gunicorn → Docker → Trivy → ECR → GitOps pull request → Argo CD. |
| Decisions | Separate application/deployment repositories; digest promotion; explicit release dispatch. |
| Security | Non-root read-only runtime, dropped capabilities, short-lived AWS identity, and scoped GitHub App promotion. |
| Automation | Application tests, image gate, container smoke test, chart validation, and promotion script. |
| Reliability | Startup/readiness/liveness probes, bounded rolling updates, disruption budget, and Git-based rollback procedure. |
| Stack | Python, Docker, GitHub Actions, Trivy, ECR, Helm, Argo CD, Kubernetes. |
| Status | Application and delivery code implemented; AWS/ECR/Argo CD integration requires environment setup. |

## GitHub analytics

<details>
<summary>Public activity and repository languages</summary>

![GitHub stats](https://github-readme-stats.vercel.app/api?username=expertnafees-hub&theme=github_dark&hide_border=true&hide_rank=true)

![Top languages](https://github-readme-stats.vercel.app/api/top-langs/?username=expertnafees-hub&theme=github_dark&hide_border=true&layout=compact)

These [third-party cards](https://github.com/anuraghazra/github-readme-stats) are best-effort and can be rate-limited or unavailable. Reliable hosting requires separate configuration. Language distribution describes repository contents, not proficiency.

</details>

## Contribution activity

<details>
<summary>Contribution visualization</summary>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/expertnafees-hub/expertnafees-hub/output/github-contribution-grid-snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/expertnafees-hub/expertnafees-hub/output/github-contribution-grid-snake.svg">
  <img alt="Contribution snake for expertnafees-hub" src="https://raw.githubusercontent.com/expertnafees-hub/expertnafees-hub/output/github-contribution-grid-snake.svg">
</picture>

Generated by the repository workflow; available after its first successful run.

</details>

## Contact & collaboration

I welcome discussion of AWS architecture, Terraform module boundaries, Kubernetes delivery, and infrastructure automation.

[GitHub](https://github.com/expertnafees-hub) · [Public repositories](https://github.com/expertnafees-hub?tab=repositories)

Use the relevant project's issue tracker for reproducible problems or proposed improvements.
