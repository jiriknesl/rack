# Do not use this fork

This was a temporary fork of [`sinkingsugar/rack`](https://github.com/sinkingsugar/rack) created to investigate whether a few targeted patches could make VST3 instrument hosting work for [vstest](https://github.com/jiriknesl/vstest).

It turned out the rack 0.4.8 codebase has multiple stacked bugs in its VST3 path on macOS, and even with three correct patches applied (defense check, `setBusArrangements`, element-wise `channelBuffers32` copy) a deeper heap-management issue around `HostProcessData::prepare()` remains. The fork is not in a usable state.

The patches **are** independently correct and should be upstreamed; the bugs they fix are real:

| Commit | Fix |
|--------|-----|
| `bd4f5ce` | Defense check rejected zero-input instruments unconditionally |
| `e167cf5` | `setBusArrangements` was never called; aux buses were left active |
| `b59670e` | `channelBuffers32` pointer was being overwritten instead of having its contents copied |

If you arrived here looking for VST3 hosting in Rust on macOS:
- For maturity, see [`coupler-rs/vst3-rs`](https://github.com/coupler-rs/vst3-rs).
- Or write a minimal C++ shim against the [Steinberg VST3 SDK](https://github.com/steinbergmedia/vst3sdk) directly.

This repository is archived and slated for deletion.
