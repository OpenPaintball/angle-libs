# angle-libs

Builds precompiled ANGLE shared libraries and bundles headers for distribution. This exists because prebuilt binaries are not published outside of Chrome, and building ANGLE locally is time- and disk-intensive.

## What this repo does

- Fetches ANGLE using `depot_tools` and `gclient`.
- Builds `libEGL` and `libGLESv2`.
- Packages the shared libraries, headers, and `LICENSE` into per-OS tarballs.

## CI

GitHub Actions builds on:

- Ubuntu (x64, arm64)
- macOS (arm64, Metal)
- Windows (x64, arm64)

## Revision pinning

The ANGLE revision is pinned in `REVISION` (one line). Examples:

- Branch ref: `refs/heads/main`
- Tag: `refs/tags/chrome_m124`
- Commit SHA: `3c1e0f3b7e5e6c8d9a...`

Update `REVISION` and push to change what CI builds.

## Artifacts

Each build produces a tarball named:

```text
angle-<LABEL>-<REVISION>.tar.gz
```

Contents:

- Shared libraries (`.so` / `.dylib` / `.dll`)
- Windows import libraries (`.lib`)
- Headers (`include/`)
- `LICENSE`

### Debug symbols

CI builds use `symbol_level=0`, so debug symbols are not produced or packaged. This reduces artifact size significantly.

## License

ANGLE is BSD 3-Clause. When distributing the packaged artifacts, include the ANGLE license (already bundled) and comply with any third-party licenses from bundled dependencies.

## References

Build instructions (official ANGLE DevSetup):

```text
https://chromium.googlesource.com/angle/angle/+/HEAD/doc/DevSetup.md
```

ANGLE project home:

```text
https://chromium.googlesource.com/angle/angle/
```

ANGLE build configuration defaults, including Metal on macOS:

```text
https://chromium.googlesource.com/angle/angle/+/HEAD/gni/angle.gni
```

ANGLE backend wiring for Metal/Vulkan:

```text
https://chromium.googlesource.com/angle/angle/+/HEAD/BUILD.gn
```

Chromium Dash (Stable channel releases for Windows):

```text
https://chromiumdash.appspot.com/fetch_releases?channel=Stable&platform=Windows
```
