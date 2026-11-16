# Honeybee Studio

eBPF observability for LLM workloads. We read LLM API calls at the TLS layer on each node and turn them into tokens
and estimated dollars per Kubernetes namespace, pod and model, with no code changes, proxy or SDK.

## Projects

### 🐝 [honeybeepf-llm](https://github.com/honeybee-studio/honeybeepf-llm)

A Rust eBPF agent that runs as a DaemonSet. It attaches uprobes to the TLS code apps already use, parses the
plaintext HTTP of calls to LLM providers, and exports token usage, cost, request counts and latency over
OpenTelemetry.

- **Cost per team** — tokens and estimated USD by namespace, pod, workload and model, with a bundled Grafana dashboard
  and Prometheus alerts for budgets and missed calls.
- **Providers** — OpenAI, Anthropic, Gemini, Amazon Bedrock, Azure OpenAI, Google Vertex AI and Meta, plus
  OpenAI-compatible APIs such as Groq, DeepSeek, Mistral, Together and OpenRouter; JSON and streaming.
- **Light** — agent CPU, memory and latency overhead measured with and without the agent ([benchmark](https://github.com/honeybee-studio/honeybeepf-llm/blob/main/docs/benchmark.md)).
- **Signed releases** — container image and Helm chart signed with cosign, listed on
  [Artifact Hub](https://artifacthub.io/packages/helm/honeybeepf-llm/honeybeepf-llm).

```bash
helm install honeybeepf-llm oci://ghcr.io/honeybee-studio/charts/honeybeepf-llm -n honeybeepf --create-namespace
```

## Stack

Rust · [Aya](https://aya-rs.dev) · BPF CO-RE · Kubernetes · OpenTelemetry · Prometheus
