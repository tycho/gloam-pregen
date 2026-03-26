# gloam-pregen

Pre-built [gloam](https://github.com/tycho/gloam) loaders, updated daily from
the latest Khronos XML specs.

Copy the directory you need into your project — each one is self-contained with
all required headers (platform headers, xxhash, etc.).

## Available loaders

| Directory | APIs | gloam flags |
|-----------|------|-------------|
| `vulkan/` | Vulkan (all versions, all extensions) | `--api vk c --alias --loader` |
| `gl-egl/` | GL core + GLES2 (merged) and EGL (all versions, all extensions) | `--api gl:core,gles2,egl --merge c --alias --loader` |

## Usage

Each directory contains:

- `include/` — public headers (`#include "gloam/vulkan.h"`, etc.) and
  dependencies (platform headers, xxhash)
- `src/` — implementation files to compile into your project

Add the `include/` directory to your include path and compile the `.c` files
alongside your project sources.

## Automation

A GitHub Actions workflow regenerates these files daily from the upstream
Khronos XML specs. The workflow:

1. Installs the latest release of gloam via `cargo install`
2. Fetches the newest XML specs from Khronos
3. Generates the loaders
4. Compile-checks the output with `gcc -fsyntax-only`
5. Verifies no file shrank by more than 10% (catches upstream breakage)
6. Commits and pushes only if the output changed

## Licenses

This repository contains code from multiple projects under different licenses:

| File | Project | License |
|------|---------|---------|
| `LICENSE.gloam-mit` | [gloam](https://github.com/tycho/gloam) (generated code) | MIT |
| `LICENSE.gloam-apache` | [gloam](https://github.com/tycho/gloam) (generated code) | Apache-2.0 |
| `LICENSE.khronos` | [Khronos Group](https://www.khronos.org/) (XML specs, platform headers) | Apache-2.0 OR MIT |
| `LICENSE.angle` | [ANGLE](https://github.com/google/angle) (supplemental XML specs) | BSD 3-Clause |
| `LICENSE.xxhash` | [xxHash](https://github.com/Cyan4973/xxHash) | BSD 2-Clause |
