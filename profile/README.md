# Honeybee Studio

eBPF observability for LLM workloads. We read LLM API calls at the TLS layer on each node and turn them into tokens
and estimated dollars per Kubernetes namespace, pod and model, with no code changes, proxy or SDK.

## Projects

### 🐝 [honeybeepf-llm](https://github.com/honeybee-studio/honeybeepf-llm)

A Rust eBPF agent that runs as a DaemonSet. It attaches uprobes to OpenSSL's `SSL_write` and `SSL_read`, parses the
plaintext HTTP of calls to LLM providers, and exports token usage, cost, request counts and latency over
OpenTelemetry.

- **Cost per team** — tokens and estimated USD by namespace, pod, workload and model, with a bundled Grafana dashboard
  and Prometheus alerts for daily budgets, spend spikes and calls that were not recorded.
- **11 provider APIs** — OpenAI, Anthropic, Gemini, Amazon Bedrock, Azure OpenAI, Google Vertex AI, Meta, and the
  OpenAI-compatible APIs of Groq, DeepSeek, Together, Fireworks, OpenRouter, Mistral and Cerebras; JSON and streaming.
- **Light** — about 53 µs of agent CPU per LLM call, measured ([benchmark](https://github.com/honeybee-studio/honeybeepf-llm/blob/main/docs/benchmark.md)).
- **Tested kernels** — Linux 5.10 to 7.2 and RHEL 8.10 / 9.6 / 9.7 in CI.
- **Signed releases** — container image and Helm chart signed with cosign, listed on
  [Artifact Hub](https://artifacthub.io/packages/helm/honeybeepf-llm/honeybeepf-llm).

```bash
helm install honeybeepf-llm oci://ghcr.io/honeybee-studio/charts/honeybeepf-llm -n honeybeepf --create-namespace
```

## Stack

Rust · [Aya](https://aya-rs.dev) · BPF CO-RE · Kubernetes · OpenTelemetry · Prometheus
