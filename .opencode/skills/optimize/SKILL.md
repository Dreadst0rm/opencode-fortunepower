---
name: optimize
description: Profile code, identify performance bottlenecks, and apply targeted optimizations
license: MIT
compatibility: opencode
metadata:
  stage: test
---

# Optimize

## When to use
- "slow", "performance issue", "too slow"
- "bottleneck", "profile this", "latency"
- "memory leak", "high CPU", "timeout"

## Workflow
1. **Profile first** — never optimize without data. Use:
   - Runtime profiler (Chrome DevTools, py-spy, pprof, perf)
   - Benchmark harness (benchmark.js, pytest-benchmark, Go benchmarks)
   - Logging with timestamps for rough measurements
2. **Identify the bottleneck** — find the slowest 20% of code (Pareto principle)
3. **Propose fix** with estimated impact:
   - Algorithmic improvement (O(n^2) → O(n log n))
   - Caching/memoization
   - Lazy loading / deferred computation
   - Batching I/O operations
   - Connection pooling
4. **Benchmark before and after** to measure actual improvement
5. **Apply the fix** only if the improvement is meaningful (>10% improvement or meets the target)

## What NOT to optimize
- Code that runs once (startup, config loading)
- Code that is I/O bound when the bottleneck is the network/disk
- Premature optimization without profiling data
- Readability sacrifices for marginal gains

## Language-specific notes
- **Node.js**: `--cpu-prof`, `--heap-prof`, `clinic`, `0x`
- **Python**: `cProfile`, `py-spy`, `pytest-benchmark`, `timeit`
- **Rust**: `cargo bench`, `perf`, `flamegraph`
- **Go**: `pprof`, `benchstat`, `trace`

## Verification
- Before and after benchmark numbers are recorded
- The optimization does not change correctness (all tests pass)
- The optimization is documented with a comment explaining why
