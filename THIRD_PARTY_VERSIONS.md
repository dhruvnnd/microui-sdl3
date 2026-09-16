# Third-party code

## microui

- Upstream: https://github.com/rxi/microui
- Pinned commit: `0850aba` (tagged "Version 2.02")
- Location: `vendor/microui/microui.c`, `vendor/microui/microui.h`,
  `vendor/microui/atlas.inl` (default font+icon atlas data, from the demo
  in the same repo)
- License: MIT, Copyright (c) 2024 rxi
- Vendored as a plain source copy (not a git submodule), unmodified from upstream.

## SDL3

- Upstream: https://github.com/libsdl-org/SDL
- Pinned tag: `release-3.4.16`
- Location: not vendored in-tree — fetched at configure time via CMake
  `FetchContent` in `CMakeLists.txt` when no system-provided SDL3 is found
  via `find_package`.
- License: zlib
