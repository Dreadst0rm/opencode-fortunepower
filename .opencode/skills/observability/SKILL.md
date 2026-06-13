---
name: observability
description: Implement observability patterns with structured logging, distributed tracing, and metrics
license: MIT
compatibility: opencode
metadata:
  stage: deploy
---

# Observability

## When to use
- "structured logging", "distributed tracing", "metrics collection"
- "health checks", "APM", "monitoring"
- "correlation IDs", "request tracking", "observability"

## Workflow
1. **Set up structured logging** — use structured logging with properties (Winston, structlog, Serilog, log4j, or framework equivalent)
2. **Add distributed tracing** — OpenTelemetry or equivalent for request tracking across services
3. **Configure metrics collection** — Prometheus, Datadog, or equivalent for application metrics
4. **Implement health checks** — liveness and readiness probes for Kubernetes
5. **Add correlation IDs** — propagate correlation IDs across services for request tracking

## Structured Logging
- Use structured logging with properties (not plain text)
- Include correlation IDs in log entries
- Never log sensitive data (passwords, tokens, PII)
- Use appropriate log levels (Debug, Information, Warning, Error, Critical)
- Be mindful of logging overhead in hot paths

## Distributed Tracing
- Use OpenTelemetry or equivalent for distributed tracing
- Add instrumentation for HTTP client/server, database, and framework
- Propagate trace context across service boundaries
- Configure exporters (Jaeger, Zipkin, Prometheus)

## Metrics
- Track business metrics (orders, users, revenue) separately from technical metrics
- Track technical metrics (request count, duration, error rate)
- Use histograms for duration distributions
- Use counters for event totals
- Use gauges for current state

## Health Checks
- Implement liveness probes — is the app running?
- Implement readiness probes — is the app ready to serve traffic?
- Check database connectivity, cache connectivity, external service availability
- Return appropriate HTTP status codes (200 for healthy, 503 for unhealthy)

## Correlation IDs
- Generate correlation ID at request entry point
- Propagate correlation ID across service boundaries (HTTP headers, message headers)
- Include correlation ID in all log entries
- Use correlation ID for request tracing across services

## Verification
- Structured logging is configured with correlation IDs
- Distributed tracing is configured with exporters
- Metrics are collected and exposed
- Health checks are implemented (liveness and readiness)
- Correlation IDs are propagated across services
- No sensitive data is logged
