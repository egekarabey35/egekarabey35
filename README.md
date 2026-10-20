# Hi, I'm Ege Karabey 👋

**Junior DevOps & Cloud Engineer** | AWS · Terraform · Kubernetes · CI/CD · Go · Linux

Information Security graduate (İstanbul Bilgi University, 2026), AWS Certified Cloud Practitioner, preparing for Solutions Architect – Associate. I build hands-on lab projects around infrastructure as code, CI/CD security gates, and Kubernetes hardening.

📍 İzmir / İstanbul · [LinkedIn](https://www.linkedin.com/in/egekarabeycsp/) · egekarabey35@gmail.com

## Projects

### [aws-terraform-hardened-infra](https://github.com/egekarabey35/aws-terraform-hardened-infra)
Multi-AZ AWS setup with Terraform: 2 public / 2 private subnets, ALB, Auto Scaling Group (2–4 instances) in private subnets.
- IMDSv2 enforced on launch templates (`http_tokens = "required"`, hop limit 1)
- Security groups allow app traffic only from the ALB security group
- GitHub Actions runs `terraform fmt`, `tflint`, `tfsec` on every push/PR

### [falco-runtime-security](https://github.com/egekarabey35/falco-runtime-security)
Falco (eBPF) with custom rules for shell spawns, secret reads and unexpected outbound connections, plus a Go worker that labels the pod and a deny-all NetworkPolicy cuts its traffic.
- Tuned rules from ~142 to <2 alerts/hour on a test workload [kendi ölçümün]

### [compliance-as-code-pipeline](https://github.com/egekarabey35/compliance-as-code-pipeline)
GitHub Actions pipeline with Checkov, OPA/Conftest and Trivy gates; AWS access via OIDC (no static keys); actions pinned to commit SHAs; Cosign keyless signing.

### [k8s-gitops-zero-trust](https://github.com/egekarabey35/k8s-gitops-zero-trust)
ArgoCD GitOps on a `kind` cluster: Pod Security Standards (Restricted), default-deny NetworkPolicies, kube-linter gate in CI.

### [trc20-vault-webhook-gateway](https://github.com/egekarabey35/trc20-vault-webhook-gateway)
Go webhook service with constant-time HMAC-SHA256 verification, Redis-based idempotency/replay protection, Vault for secrets, Docker + NetworkPolicies.

## Stack
AWS (EC2, VPC, IAM, KMS, S3, CloudWatch) · Terraform · Docker · Kubernetes · ArgoCD · GitHub Actions · Falco · Linux · Go · Bash · Python

> All projects are lab/portfolio work, not production systems.
