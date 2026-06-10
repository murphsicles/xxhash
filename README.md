# @crypto/xxhash

Pure Zeta port of [xxhash-rust](https://crates.io/crates/xxhash-rust) v0.8.15.

Provides xxh32, xxh64, and xxh3 hash functions for checksumming.

## Usage

```
use @crypto/xxhash::xxh64;

fn checksum(data: &[u8]) -> u64 {
    return xxh64::xxh64(data, 0);
}
```

## Modules

- `xxh32` — XXH32 one-shot + streaming
- `xxh64` — XXH64 one-shot + streaming
- `xxh3` — XXH3 one-shot + streaming (fastest)
- `const_xxh32` — const-compatible XXH32
- `const_xxh64` — const-compatible XXH64
- `const_xxh3` — const-compatible XXH3
