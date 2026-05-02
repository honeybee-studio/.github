# Honeybee Studio

Lightweight eBPF-based observability for AI/LLM workloads. Kernel-level visibility into what models cost, where they spend, and what they leak — without code changes.

## Projects

### 🐝 [honeybeepf-llm](https://github.com/honeybee-studio/honeybeepf-llm) — LLM API tracing
Production-ready agent that hooks `libssl` via uprobes to capture LLM API calls (OpenAI, Anthropic, Google) and emit per-process token / latency metrics. No SDK, no proxy, no app changes.

### 🛣️ Roadmap

- **honeybeepf-gpu** — Per-process GPU cost attribution. eBPF on `libcuda.so` + NVML power telemetry → real-time `₩/min` overlay per training job. Energy-aware MLOps.
- **honeybeepf-anonymizer** — In-flight PII redaction on captured LLM traffic. Compliance-ready (GDPR, internal data policy).
- **honeybeepf** — Enterprise distribution. License-gated bundle of the above with verifier and unified deploy.

## Why eBPF

- **Zero app changes** — instrument any binary, any framework, any language.
- **Low overhead** — kernel-side capture, userspace processing.
- **Standard pipelines** — OpenTelemetry export, Prometheus metrics, K8s DaemonSet.

## Stack

Rust · [Aya](https://aya-rs.dev) · BPF CO-RE · Kubernetes · OpenTelemetry
