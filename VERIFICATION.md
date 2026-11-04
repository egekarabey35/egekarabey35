# Portfolio Verification Matrix — 2026-11-04

This document distinguishes **tested code** from **external environments not yet tested**. GitHub Actions records are linked so reviewers can audit the results themselves.

| Repository | Tested automatically | Latest verified evidence | Remaining external verification |
| --- | --- | --- | --- |
| [AWS Terraform](https://github.com/egekarabey35/aws-terraform-hardened-infra) | `terraform fmt`, `init -backend=false`, `validate`, TFLint, tfsec; CI references immutable action commits. | [Successful CI run](https://github.com/egekarabey35/aws-terraform-hardened-infra/actions/runs/41742675574) | AWS identity, account/region quotas, actual `plan` and `apply`, KMS/ASG bootstrap, ALB access and real billing |
| [Kubernetes GitOps](https://github.com/egekarabey35/k8s-gitops-zero-trust) | Kube-Linter, published-image digest resolution and successful disposable Kind workload startup plus Restricted Pod Security Admission rejection. | [Kind workload and admission proof](https://github.com/egekarabey35/k8s-gitops-zero-trust/actions/runs/41743308105) and [lint/image registry proof](https://github.com/egekarabey35/k8s-gitops-zero-trust/actions/runs/41743308055) | NetworkPolicy packet enforcement requires Calico/Cilium; Argo CD deployment and full drift reconciliation require a configured cluster |
| [Falco Runtime](https://github.com/egekarabey35/falco-runtime-security) | Go test/vet, unauthorized and oversized webhook requests, bounded worker queue, mocked Kubernetes API label patch. | [Successful Go test run](https://github.com/egekarabey35/falco-runtime-security/actions/runs/41742504849) | Live Falco/eBPF detection, rules deployment, external ingress, CNI quarantine enforcement, latency/noise metrics |
| [Compliance-as-Code](https://github.com/egekarabey35/compliance-as-code-pipeline) | Positive/negative OPA/Conftest policy fixtures, Python evidence collector unit tests and fail-closed behavior. | [Successful policy/evidence test](https://github.com/egekarabey35/compliance-as-code-pipeline/actions/runs/41742162501) | Actual cloud OIDC role/backend, end-to-end Checkov/Trivy/Gitleaks audit pipeline, Cosign attestation, independent PCI/SOC2 auditors |
| [TRC-20 Webhook](https://github.com/egekarabey35/trc20-vault-webhook-gateway) | Go race/unit tests, vet, Docker build, Docker Compose, signed HTTP/Redis requests, canonicalized duplicate rejection, invalid signature/field tests; Kubernetes API NetworkPolicy selector validation. | [Successful Docker integration](https://github.com/egekarabey35/trc20-vault-webhook-gateway/actions/runs/41743804113) and [Kubernetes policy API validation](https://github.com/egekarabey35/trc20-vault-webhook-gateway/actions/runs/41743741387) | Real TRON blockchain confirmations, transaction settlement, full Vault Agent and Kubernetes deployment, durable reconciliation |

## Reproducible checks

For AWS static checks (no provisioning):
```sh
terraform fmt -check
terraform init -backend=false
terraform validate
tflint --init && tflint -f compact
```

For Falco remediation worker:
```sh
cd remediation
go test ./...
go vet ./...
```

For TRC-20:
```sh
go test -race ./...
go vet ./...
docker build -t trc20-gateway:local .
# The GitHub Actions workflow also launches Docker Compose and runs
# scripts/smoke_compose.py against live local HTTP/Redis containers.
```

For Compliance-as-Code (in the nested project folder):
```sh
python3 -m unittest discover -s tests -v
conftest test infrastructure/prod/compliant-deployment.yaml -p policies/opa -n compliance.pci_dss
# Expected to fail:
conftest test test-workloads/negative-fixtures/non-compliant-deployment.yaml -p policies/opa -n compliance.pci_dss
```

## Rules for security claims

- A **green CI badge** only proves the recorded CI checks, not an external infrastructure deployment.
- Sample SHA256 image digests should resolve against an OCI registry; test their existence in CI.
- Never include real access tokens, credential files, secrets or personally identifying test records in repositories or CI logs.
- Portfolios demonstrate learning and implemented checks; none of these labs claims financial settlement or external compliance certification.
