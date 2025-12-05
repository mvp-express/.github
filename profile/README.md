# MVP.Express GitHub Organization

## Welcome to MVP.Express

We build production-grade Java infrastructure for systems where every microsecond counts. Our libraries are built entirely on the Foreign Function & Memory (FFM) API, providing memory safety and deterministic performance for high-frequency trading, real-time systems, and ultra-low-latency applications.

[Sponsor the project](https://github.com/sponsors/mvp-express)

**Zero GC. Zero Allocation. Zero Copy. Ultra-Low Latency.**

---

## Projects

### roray-ffm-utils

The foundational layer of the MYRA stack. `roray-ffm-utils` provides memory management primitives built on FFM, including off-heap memory arenas, direct buffer operations, and safe native resource lifecycle management. It abstracts the complexity of FFM's low-level APIs while maintaining full control over memory layout and allocation patterns. This enables deterministic performance by eliminating heap allocations from the critical path. The library handles Arena lifecycle, MemorySegment pooling, and provides utilities for zero-copy memory access patterns — all without relying on `Unsafe` or JNI boilerplate.

**Key Features:**
- Memory arenas for predictable off-heap allocation
- Direct buffer utilities with bounds checking
- Native resource lifecycle management
- Zero-copy memory access patterns
- Full FFM API abstraction layer

---

### myra-codec

A zero-copy, schema-driven serialization framework for ultra-high-throughput message processing. `myra-codec` generates efficient Java code from YAML schema definitions, enabling direct reads and writes to off-heap memory without intermediate object allocation. It leverages the flyweight pattern — objects are stateless views over MemorySegments, providing field access through pointer arithmetic and structured layout interpretation. This approach achieves 2-3x throughput improvements over traditional codecs (Kryo, FlatBuffers) on decode-heavy workloads while maintaining sub-allocation latencies. The generated code is human-readable and JIT-friendly, with no reflection overhead.

**Key Features:**
- Schema-driven code generation (YAML → Java)
- Flyweight pattern for zero-copy deserialization
- Direct off-heap memory reading/writing
- 4.1M+ ops/sec decode throughput (order book workload)
- Predictable latency with no GC pressure

---

### myra-transport

A high-performance networking library built on Linux `io_uring`, designed for sub-30μs ping-pong latencies. `myra-transport` abstracts io_uring's ring buffer model while providing multiple completion strategies (polling, token-based tracking, sq-polling) to optimize for different workload patterns. It eliminates traditional syscall overhead by batching I/O operations in shared kernel rings, reducing context switches and enabling higher throughput with lower latency variance. The library handles connection management, buffer pooling, and provides FFM-native MemorySegment integration for zero-copy networking. MYRA_TOKEN mode achieves 27% lower latency than Netty while maintaining 37% higher throughput.

**Key Features:**
- Linux `io_uring` integration
- Multiple completion strategies (normal, SQPOLL, token-based)
- Sub-30μs mean latencies with controlled tail behavior
- Zero-copy network I/O via FFM MemorySegments
- 34.8K+ ops/sec throughput vs Netty's 25.4K ops/sec
- Connection and buffer pooling optimizations

---

## Roadmap

- **MVP.Express RPC** (In Design Phase) — MYRA Virtual Procedure over Express Link. A lightweight RPC framework combining myra-codec and myra-transport for ultra-low-latency microservices.
- **JIA-Cache** (In Design Phase) — Java In-Memory Accelerated Cache. Off-heap caching with predictable latency for real-time systems.

---

## Getting Started

Each project includes:
- Comprehensive README with setup instructions
- JMH benchmarks for reproducibility
- Example usage and integration guides
- Detailed API documentation

Start with `roray-ffm-utils` for memory management primitives, then layer `myra-codec` and `myra-transport` based on your application's needs.

---

## License & Sponsorship

All MYRA libraries are **free and open source** (Apache 2.0). No enterprise tier, no gated features. Development is sustained through open sponsorships from individuals and organizations who value deterministic, high-performance Java infrastructure.

[Sponsor the project](https://github.com/sponsors/mvp-express)

---

## Contact & Community

- **Issues & Discussions:** [GitHub Discussions](https://github.com/mvp-express/discussions)
- **Benchmarks & Reproducibility:** See individual project repositories for benchmark code and methodology
- **Questions?** Open an issue or start a discussion — we're here to help

**Built for teams that care about correctness, velocity, and performance.**
