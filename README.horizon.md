# FNA3D for Horizon

This fork adds a headless renderer, D3D11 exclusive-fullscreen handling, and an
OpenGL-only build option for Horizon. It incorporates Popax21's exclusive-fullscreen
patch and psyGamer's headless patch from
[Everest-libs](https://github.com/EverestAPI/Everest-libs/tree/3311fc9/patches),
preserving their source notices. `BUILD_VULKAN` defaults to ON; the Horizon build
sets it to OFF. Headless rendering must be selected explicitly.
Upstream: [FNA-XNA/FNA3D](https://github.com/FNA-XNA/FNA3D), zlib license;
retain the upstream license and file notices. The port uses public devkitPro/libnx
homebrew interfaces. No Nintendo SDK is required.

## Build

On Linux, install Python 3.12+, Git, CMake, Ninja, make and devkitPro's switch-dev
and switch-portlibs packages. Set `DEVKITPRO` and put devkitA64/bin and tools/bin
on PATH. Build from any directory:

```sh
python3 build-horizon.py --jobs 8
```

The script fetches and builds pinned [libnx](https://github.com/pixelomer/libnx)
in ignored `artifacts/sources/`; it does not install over the system SDK.
`--libnx /path/to/sdk` optionally reuses a built SDK. Build outputs are under `artifacts/horizon/`. Keep symbols for application debugging.
Full commit pins are in `eng/horizon/dependencies.json` and Git submodule entries.
`--source-mirrors FILE.json` can map canonical URLs to local Git source mirrors;
mirrors supply source objects, never prebuilt libraries.

Archive output: `libFNA3D.a`, `libmojoshader.a`.
Applications can use this library through [FNA](https://github.com/pixelomer/FNA).
These builds use SDL2/OpenGL and do not enable a Vulkan renderer.

The source-build helpers' recursive source-fetch controls can be run with
`python3 tests/horizon/test_sources.py`; these tests create only temporary,
original Git fixtures and do not require a console or game files.
