# Pipe

A dummy [Tauri](https://tauri.app/) application using [SurrealDB](https://surrealdb.com/).

This is a minimal test to debug a crash whilst compiling [rocksdb](https://github.com/rust-rocksdb/rust-rocksdb) on MacOS.


## MacOS

- OS: 12.6.1
- Tauri: 1.2.2
- SurrealDB: 1.0.0-beta.8
- Rust: 1.65.0 (897e37553 2022-11-02)
- GCC: Apple clang version 14.0.0 (clang-1400.0.29.202)


Note that a crate with just SurrealDB works fine. The combination of Tauri and SurrealDB is what makes it crash.


## Error

```
The following warnings were emitted during compilation:

warning: In file included from rocksdb/cache/fast_lru_cache.cc:10:
warning: rocksdb/cache/fast_lru_cache.h:165:3: error: aligned deallocation function of type 'void (void *, std::align_val_t) noexcept' is only available on macOS 10.14 or newer
warning:   ~LRUCacheShard() override = default;
warning:   ^
warning: rocksdb/cache/fast_lru_cache.cc:439:18: note: in defaulted destructor for 'rocksdb::fast_lru_cache::LRUCacheShard' first required here
warning:       shards_[i].~LRUCacheShard();
warning:                  ^
warning: rocksdb/cache/fast_lru_cache.h:165:3: note: if you supply your own aligned allocation functions, use -faligned-allocation to silence this diagnostic
warning:   ~LRUCacheShard() override = default;
warning:   ^
warning: In file included from rocksdb/cache/lru_cache.cc:10:
warning: rocksdb/cache/lru_cache.h:305:11: error: aligned deallocation function of type 'void (void *, std::align_val_t) noexcept' is only available on macOS 10.14 or newer
warning:   virtual ~LRUCacheShard() override = default;
warning:           ^
warning: rocksdb/cache/lru_cache.cc:666:18: note: in defaulted destructor for 'rocksdb::lru_cache::LRUCacheShard' first required here
warning:       shards_[i].~LRUCacheShard();
warning:                  ^
warning: rocksdb/cache/lru_cache.h:305:11: note: if you supply your own aligned allocation functions, use -faligned-allocation to silence this diagnostic
warning:   virtual ~LRUCacheShard() override = default;
warning:           ^
warning: 1 error generated.
warning: 1 error generated.

error: failed to run custom build command for `librocksdb-sys v0.8.0+7.4.4`

Caused by:
  process didn't exit successfully: `/Users/arnau/kitchen/lab/tauri_baseline/pipe/src-tauri/target/debug/build/librocksdb-sys-b20a356a5f858d23/build-script-build` (exit status: 1)
  --- stdout
  cargo:rerun-if-changed=rocksdb/
  TARGET = Some("x86_64-apple-darwin")
  OPT_LEVEL = Some("0")
  HOST = Some("x86_64-apple-darwin")
  cargo:rerun-if-env-changed=CXX_x86_64-apple-darwin
  CXX_x86_64-apple-darwin = None
  cargo:rerun-if-env-changed=CXX_x86_64_apple_darwin
  CXX_x86_64_apple_darwin = None
  cargo:rerun-if-env-changed=HOST_CXX
  HOST_CXX = None
  cargo:rerun-if-env-changed=CXX
  CXX = None
  cargo:rerun-if-env-changed=CXXFLAGS_x86_64-apple-darwin
  CXXFLAGS_x86_64-apple-darwin = None
  cargo:rerun-if-env-changed=CXXFLAGS_x86_64_apple_darwin
  CXXFLAGS_x86_64_apple_darwin = None
  cargo:rerun-if-env-changed=HOST_CXXFLAGS
  HOST_CXXFLAGS = None
  cargo:rerun-if-env-changed=CXXFLAGS
  CXXFLAGS = None
  cargo:rerun-if-env-changed=CRATE_CC_NO_DEFAULTS
  CRATE_CC_NO_DEFAULTS = None
  DEBUG = Some("true")
  CARGO_CFG_TARGET_FEATURE = Some("fxsr,sse,sse2,sse3,ssse3")
  cargo:rerun-if-env-changed=CXX_x86_64-apple-darwin
  CXX_x86_64-apple-darwin = None
  cargo:rerun-if-env-changed=CXX_x86_64_apple_darwin
  CXX_x86_64_apple_darwin = None
  cargo:rerun-if-env-changed=HOST_CXX
  HOST_CXX = None
  cargo:rerun-if-env-changed=CXX
  CXX = None
  cargo:rerun-if-env-changed=CXXFLAGS_x86_64-apple-darwin
  CXXFLAGS_x86_64-apple-darwin = None
  cargo:rerun-if-env-changed=CXXFLAGS_x86_64_apple_darwin
  CXXFLAGS_x86_64_apple_darwin = None
  cargo:rerun-if-env-changed=HOST_CXXFLAGS
  HOST_CXXFLAGS = None
  cargo:rerun-if-env-changed=CXXFLAGS
  CXXFLAGS = None
  cargo:rerun-if-env-changed=CRATE_CC_NO_DEFAULTS
  CRATE_CC_NO_DEFAULTS = None
  CARGO_CFG_TARGET_FEATURE = Some("fxsr,sse,sse2,sse3,ssse3")
  cargo:rerun-if-env-changed=CXX_x86_64-apple-darwin
  CXX_x86_64-apple-darwin = None
  cargo:rerun-if-env-changed=CXX_x86_64_apple_darwin
  CXX_x86_64_apple_darwin = None
  cargo:rerun-if-env-changed=HOST_CXX
  HOST_CXX = None
  cargo:rerun-if-env-changed=CXX
  CXX = None
  cargo:rerun-if-env-changed=CXXFLAGS_x86_64-apple-darwin
  CXXFLAGS_x86_64-apple-darwin = None
  cargo:rerun-if-env-changed=CXXFLAGS_x86_64_apple_darwin
  CXXFLAGS_x86_64_apple_darwin = None
  cargo:rerun-if-env-changed=HOST_CXXFLAGS
  HOST_CXXFLAGS = None
  cargo:rerun-if-env-changed=CXXFLAGS
  CXXFLAGS = None
  cargo:rerun-if-env-changed=CRATE_CC_NO_DEFAULTS
  CRATE_CC_NO_DEFAULTS = None
  CARGO_CFG_TARGET_FEATURE = Some("fxsr,sse,sse2,sse3,ssse3")

  ... output elided ...

  --- stderr

  error occurred: Command "c++" "-O0" "-ffunction-sections" "-fdata-sections" "-fPIC" "-gdwarf-2" "-fno-omit-frame-pointer" "-m64" "-arch" "x86_64" "-I" "rocksdb/include/" "-I" "rocksdb/" "-I" "rocksdb/third-party/gtest-1.8.1/fused-src/" "-I" "snappy/" "-I" "lz4/lib/" "-I" "/Users/arnau/.cargo/registry/src/github.com-1ecc6299db9ec823/zstd-sys-2.0.4+zstd.1.5.2/zstd/lib" "-I" "/Users/arnau/kitchen/lab/tauri_baseline/pipe/src-tauri/target/debug/build/libz-sys-c2273ef22ddd682c/out/include" "-I" "/Users/arnau/kitchen/lab/tauri_baseline/pipe/src-tauri/target/debug/build/bzip2-sys-392333b6740e61f6/out/include" "-I" "." "-Wall" "-Wextra" "-std=c++17" "-Wsign-compare" "-Wshadow" "-Wno-unused-parameter" "-Wno-unused-variable" "-Woverloaded-virtual" "-Wnon-virtual-dtor" "-Wno-missing-field-initializers" "-Wno-strict-aliasing" "-Wno-invalid-offsetof" "-msse2" "-std=c++17" "-DSNAPPY=1" "-DLZ4=1" "-DZSTD=1" "-DZLIB=1" "-DBZIP2=1" "-DNDEBUG=1" "-DOS_MACOSX" "-DROCKSDB_PLATFORM_POSIX" "-DROCKSDB_LIB_IO_POSIX" "-DROCKSDB_SUPPORT_THREAD_LOCAL" "-DHAVE_UINT128_EXTENSION=1" "-o" "/Users/arnau/kitchen/lab/tauri_baseline/pipe/src-tauri/target/debug/build/librocksdb-sys-97ad3ca1c0e0ad6a/out/rocksdb/cache/fast_lru_cache.o" "-c" "rocksdb/cache/fast_lru_cache.cc" with args "c++" did not execute successfully (status code exit status: 1).
```
