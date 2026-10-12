# Android 16 KB page size

Google Play requires 64-bit native libraries (`arm64-v8a`, `x86_64`) to use
16 KB ELF `PT_LOAD` alignment.

## What changed

`android/libs/fijkplayer-full-release.aar` is based on
`com.befovy.fijkplayer:fijkplayer-full:0.7.16`, with only the `x86_64` natives
replaced by 16 KB-aligned builds from
[`gsyvideoplayer-x64:14.0.0`](https://github.com/CarGuo/GSYVideoPlayer)
(`libijkffmpeg.so`, `libijkplayer.so`, `libijksdl.so`).

Upstream `arm64-v8a` libs already had ≥16 KB alignment and were kept as-is.

## Rebuild the AAR

```bash
# download AARs, replace jni/x86_64/*.so, re-zip into android/libs/
# Align must show 0x4000:
llvm-readelf -lW jni/x86_64/libijkffmpeg.so | grep LOAD
```
