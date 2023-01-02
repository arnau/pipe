# Pipe

A dummy [Tauri](https://tauri.app/) application using ~~[SurrealDB](https://surrealdb.com/)~~ [RocksDB](https://rocksdb.org/).

This is a minimal test to verify a crash whilst compiling Tauri with [rocksdb](https://github.com/rust-rocksdb/rust-rocksdb) as a dependency on MacOS.

There are two GitHub actions jobs configured: `build` and `phased`, the first fails on MacOS whilst the latter succeeds.

The `build` job runs on three targets: Windows MSVC, Linux and MacOS (x86). Besides installing dependencies it just runs `npm run tauri build`. However, it [fails when compiling on MacOS](https://github.com/arnau/pipe/actions/runs/3668831344/jobs/6202223727).

The `phase` job runs on MacOS, installs dependencies and runs the build in two steps:

1. Compiles `src-tauri` with `cargo build --release`.
2. Compiles the rest with `npm run tauri build`.

This [approach works fine](https://github.com/arnau/pipe/actions/runs/3822299743/jobs/6502296848) which makes me think something is off with Tauri's build step.

