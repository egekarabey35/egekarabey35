# Hi, I'm Ege Karabey 👋
**Cloud Security & DevSecOps Engineer | Building Fail-Closed Systems**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/egekarabeycsp/)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat&logo=gmail&logoColor=white)](mailto:egekarabey35@gmail.com)
[![Location](https://img.shields.io/badge/Location-Izmir%2C%20Turkey-blue?style=flat&logo=google-maps&logoColor=white)](#)

Engineering resilient infrastructure with **Terraform**, enforcing Zero-Trust at the container layer (**Kubernetes**), and intercepting threats at kernel level (**eBPF / Falco**). Focused on eliminating "security theater" by replacing permissive defaults with strict, audit-ready compliance-as-code controls.

---

### 🛡️ Core Engineering Principles
* **Fail-Closed by Design:** CI/CD pipelines block on critical misconfigurations rather than generating passive warnings.
* **Kernel & Runtime Grounding:** Static code analysis is backed by live eBPF telemetry to catch drift and container breakouts.
* **Identity-First Security:** No long-lived credentials. All cloud operations leverage short-lived tokens via OIDC.

---

### 🚀 Featured Architecture & Hardened Repositories

#### 1. [aws-terraform-hardened-infra](https://github.com/egekarabey35/aws-terraform-hardened-infra)
> Modular, audit-ready AWS infrastructure provisioned via Terraform with SOC2/PCI-DSS guardrails.

* **Capital One Vector Mitigation:** Enforced IMDSv2 (`http_tokens = "required"`) across all EC2 Launch Templates to eliminate SSRF-based metadata credential theft.
* **Cryptographic Lifecycle:** Automated annual key rotation (`enable_key_rotation = true`) across Customer Managed KMS Keys.
* **State Concurrency:** Multi-environment S3 backend with atomic DynamoDB table locking.

```text
[EC2 / Launch Template] ──(IMDSv2 Required)──> [No Metadata SSRF Token Leak]
          │
          └──(Private Subnet)──> [NAT Gateway] ──> [Restricted Egress Only]
```

---

#### 2. [falco-runtime-security](https://github.com/egekarabey35/falco-runtime-security)
> Kernel-level runtime detection with automated dynamic network quarantine in Kubernetes.

* **eBPF System Call Inspection:** Intercepts suspicious process executions (`execve`, shell spawns) and privilege escalation attempts at the kernel layer.
* **Automated Remediation Loop:** Event triggers a dynamic controller applying an egress-blocking `NetworkPolicy` to isolate the compromised pod within milliseconds.

```text
[Container Breakout Attempt]
          │ (eBPF Probe)
          ▼
    [Falco Engine] ──(Alert Trigger)──> [Remediation Daemon]
                                                │
                                                ▼
                                    [Apply NetworkPolicy]
                                   (Pod Isolated Instantly)
```

---

#### 3. [compliance-as-code-pipeline](https://github.com/egekarabey35/compliance-as-code-pipeline)
> Zero-trust CI/CD engine enforcing Shift-Left policy validation and supply chain security.

* **Keyless AWS Authentication:** Integrated AWS IAM with GitHub Actions via OpenID Connect (OIDC), removing static access keys from repositories.
* **Supply Chain Hardening:** Pinned all third-party GitHub Actions to immutable full-length commit SHAs instead of mutable version tags.
* **Blocking Gates:** Checkov and Open Policy Agent (OPA) scans configured to exit with non-zero status codes on critical vulnerabilities.

---

#### 4. [k8s-gitops-zerotrust](https://github.com/egekarabey35/k8s-gitops-zerotrust)
> Declarative Kubernetes cluster architecture with strict network isolation.

* **Default-Deny Posture:** Enforced explicit ingress and egress NetworkPolicies across all namespaces.
* **Least-Privilege RBAC:** ServiceAccounts scoped strictly to operational requirements, restricting access to cluster API endpoints.

---

#### 5. [trc20-vault-webhook-gateway](https://github.com/egekarabey35/trc20-vault-webhook-gateway)
> Cryptographically verified, idempotent transaction processing service.

* **Signature Verification:** Validates HMAC-SHA256 payloads against replay attacks using sliding window timestamps.
* **Container Hardening:** Minimal multi-stage distroless base image running as an unprivileged non-root user.

---

### 🧰 Technical Arsenal

| Domain | Stack / Technologies |
| :--- | :--- |
| **Cloud Platforms** | AWS (VPC, IAM, KMS, EC2, S3, CloudWatch, EKS basics) |
| **Infrastructure as Code** | Terraform, HCL, Remote State Architecture |
| **Containers & Orchestration** | Docker, Kubernetes, NetworkPolicies, Helm, GitOps |
| **Security & Compliance** | Falco (eBPF), Checkov, OPA / Rego, IMDSv2, KMS Rotation |
| **CI/CD & Automation** | GitHub Actions (OIDC, SHA Pinning), Bash, Python |
| **Operating Systems** | Linux (Ubuntu, Debian), POSIX shell debugging |

---

### 📜 Formal Audits & Verification
All featured projects include dedicated `AUDIT_REVIEW_SIGNOFF.md` documents detailing security trade-offs, failed test cases, and post-remediation evidence.
