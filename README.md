# nimsimd

![Github Actions](https://github.com/guzba/nimsimd/workflows/Github%20Actions/badge.svg)

`nimble install nimsimd`

This repo provides pleasant Nim bindings for various SIMD instructions.

Each SIMD instruction set is in its own file for importing.

## Status

This repo is under development. Check back here for the latest status.

## x86

Instruction Set | Bindings
--- | ---:
SSE | ✅
SSE2 | ✅
SSE3 | ✅
SSSE3 | ✅
SSE4.1 | ✅
SSE4.2 | ✅
AVX | ✅
AVX2 | ✅
PCLMULQDQ | ✅

### Compiler flags

Some instruction sets require additional compiler flags to compile. I suggest
putting any code that uses these instructions into its own .nim file and adding a `localPassc` pragma to the top of that file as needed, such as:

```nim
import nimsimd/sse42

when defined(gcc) or defined(clang):
  {.localPassc: "-msse4.2".}

...
```

### Runtime check

You can also check if instruction sets are available at runtime:

```nim
import nimsimd/runtimecheck

echo checkInstructionSets({SSE41, PCLMULQDQ})
```

## ARM

NEON bindings are started but experimental. Much to learn here about versioning and compilers.

## Uses of nimsimd

* [Noisy](https://github.com/guzba/noisy) uses SIMD to accelerate generating coherent noise.
* [Pixie](https://github.com/treeform/pixie) uses SIMD for faster 2D drawing.

## Testing

`nimble test`
