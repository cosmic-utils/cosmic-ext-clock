# Clock

[![Sponsor](https://img.shields.io/badge/sponsor-FreddyFunk-ea4aaa?logo=github-sponsors)](https://github.com/sponsors/FreddyFunk)
[![CI](https://github.com/cosmic-utils/cosmic-ext-clock/actions/workflows/ci.yml/badge.svg)](https://github.com/cosmic-utils/cosmic-ext-clock/actions/workflows/ci.yml)
[![Release](https://github.com/cosmic-utils/cosmic-ext-clock/actions/workflows/release.yml/badge.svg)](https://github.com/cosmic-utils/cosmic-ext-clock/actions/workflows/release.yml)
[![Translation status](https://hosted.weblate.org/widget/cosmic-utils/clock/svg-badge.svg)](https://hosted.weblate.org/engage/cosmic-utils/)

A responsive clock application for COSMIC desktops and Linux phones, built with [libcosmic](https://github.com/pop-os/libcosmic).

<p>
  <img src="resources/icons/hicolor/scalable/apps/org.cosmic_utils.clock.svg" alt="Clock app icon" width="80">
</p>

![Clock preview](preview/preview-001.png)

[View more screenshots](preview/README.md)

## Features

Alarms are evaluated while Clock is running. They are not yet backed by a system service, so closing the application also stops alarm delivery.

## Run

```bash
just run
just demo
```

`just demo` opens the deterministic world-clock page used as the basis for preview automation.

## Build and install

Requirements: Rust 1.98+, `just`, pkg-config, Wayland and XKB development libraries.

```bash
just check
just build-release
sudo just install
```

The Flatpak needs Wayland, fallback X11, DRI, PulseAudio-compatible playback, desktop notifications, read-only COSMIC configuration, and COSMIC settings-daemon access. It does not require network, location, or sensor permissions.

## Packaging and automation

The repository retains the blueprint's Flatpak, Alpine APK, cross-compilation, metadata generation, deterministic preview, CI, and release workflows. Run `just generate` after dependency or translation changes to refresh localized metadata and Flatpak Cargo sources.

Dependabot checks Cargo dependencies and GitHub Actions daily at 06:00 UTC. libcosmic updates remain individual PRs; other Cargo minor and patch updates are grouped, while major updates stay separate. Cargo updates increase manifest requirements as well as the lockfile. Rust toolchain and Python build dependencies are checked weekly on Mondays. Updates still require review and passing CI.

`rust-toolchain.toml` is the compiler-version source for CI and the musl build images. `Cargo.toml` keeps the minimum supported Rust version separately. `requirements-build.txt` supplies the Python dependencies for both local Flatpak source generation and CI; the local recipe uses an isolated uv environment or a virtualenv rather than arbitrary preinstalled modules.

Container-base updates, the coherent cross CLI/image set, rustup and generator checksum pins, and Flatpak runtime/BaseApp compatibility remain reviewed maintenance tasks. Like Camera, the preview container uses `fedora:44` and current distro packages, extracting the COSMIC theme from the repository's current `cosmic-settings` RPM. CI caches the built image by Containerfile hash. Run `just generate-previews` to regenerate screenshots and review visual changes after rebuilding: package versions are not locked, so a fresh build can change their appearance.

## License

Licensed under GPL-3.0-only. Contributions intentionally submitted for inclusion are licensed under the same terms. Source files should carry `SPDX-License-Identifier: GPL-3.0-only`.