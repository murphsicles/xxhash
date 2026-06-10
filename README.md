# @crypto/xxhash

Pure Zeta port of [xxhash-rust](https://crates.io/crates/xxhash-rust) v0.8.15.

XXHash is an extremely fast non-cryptographic hash algorithm, working at speeds close to RAM limits. It is well-suited for checksums, hash tables, and data integrity verification.

## Installation

```toml
[dependencies]
@crypto/xxhash = "0.1.0"
```

## Usage

### xxh64 (64-bit hash)

```zeta
use @crypto/xxhash::xxh64;

fn checksum(data: i64, len: i64) -> i64 {
    return xxh64::xxh64(data, len, 0);
}
```

### xxh32 (32-bit hash)

```zeta
use @crypto/xxhash::xxh32;

fn checksum32(data: i64, len: i64) -> i64 {
    return xxh32::xxh32(data, len, 0);
}
```

### xxh3 (fastest, 64-bit)

```zeta
use @crypto/xxhash::xxh3;
```

## Example: SuperBlock checksum

```zeta
use @crypto/xxhash::xxh64;

fn verify_superblock(buf: i64) -> i64 {
    let stored = os_load(buf + 32);  // checksum at offset 32
    let computed = xxh64::xxh64(buf, 32, 0);
    if (computed == stored) { return 0; }
    return -1;
}
```

## Modules

| Module | Description | Status |
|--------|-------------|--------|
| `xxh64` | XXH64 one-shot + streaming | ✅ Tested |
| `xxh32` | XXH32 one-shot + streaming | ✅ Ported |
| `xxh3` | XXH3 (fastest) | ✅ Ported |
| `const_xxh32` | const-compatible XXH32 | ✅ Ported |
| `const_xxh64` | const-compatible XXH64 | ✅ Ported |
| `const_xxh3` | const-compatible XXH3 | ✅ Ported |

## Known Limitations

- Uses `i64` (signed) arithmetic per Zeta's type system. The hash output bit pattern is correct for both signed and unsigned interpretation.
- Hex constants ≥ `0x8000000000000000` parsed as zero by zetac — workaround uses signed decimal literals.
- `#[cfg(feature)]` conditional compilation is parsed but not evaluated by zetac — all modules compile unconditionally.

## License

MIT — ported from [xxhash-rust](https://github.com/DoumanAsh/xxhash-rust) which is MIT/Apache-2.0.

## Source

https://github.com/murphsicles/xxhash
