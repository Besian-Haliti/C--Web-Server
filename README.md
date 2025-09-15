# Multithreaded HTTP Server (C++)
High-performance HTTP/1.1 server showcasing low-latency network I/O, thread pooling, and platform-optimized reactors (IOCP on Windows, `epoll` on Linux).


## Why this matters
- Matches low-latency C++ backend work: efficient I/O + concurrency.
- Demonstrates scalability, instrumentation, and benchmarking discipline.


## Features
- Thread pool with work-stealing
- Non-blocking I/O: **IOCP** (Windows) / **epoll** (Linux)
- Keep-alive, basic routing, static file handler
- Structured logging + metrics (RPS, p50/p90/p99 latency)
- Clean shutdown, zero-copy send where available


## Architecture
[Listener] -> [Accept Loop] -> [Conn Dispatcher] -> [Thread Pool] -> [Parser] -> [Router] -> [Handlers] |-> [Metrics] (atomic counters + histograms)


## Dependencies
- C++20, CMake, Ninja
- `asio` (or `boost-asio`), `fmt`, `spdlog`, optional `openssl`
- Tests: `gtest`


# Configure + build (Release)
cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release `
-DCMAKE_TOOLCHAIN_FILE="$env:VCPKG_ROOT\scripts\buildsystems\vcpkg.cmake"
cmake --build build
