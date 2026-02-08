# uup-converter — Nix package README

This Nix package builds the uup-converter tool that converts UUP (Unified Update Platform) downloads into Windows installation media (ISO/WIM) and related artifacts.

Repository
- Source: https://github.com/Cairnstew/uup-converter-nix
- Upstream project and licensing: consult the upstream uup-converter repository for the authoritative README, usage details, and license.

Building locally (non-flake)
- From the repository root:
    - nix-build -A uup-converter
- The build produces a `./result` symlink. The installed binary is typically at `./result/bin/uup-converter`.

Building with flakes (if you use flakes)
- nix build .#uup-converter
- The build output is available in the Nix store and linked into `./result` when using the legacy behavior or into `./result` if you run `nix build --out-link result`.

Installing
- Per-user (legacy):
    - nix-env -f . -iA uup-converter
- Declarative NixOS:
    - Add `uup-converter` to `environment.systemPackages` (or `environment.userPackages` for home-manager).

Basic usage
- General form (check `--help` for exact flags supported by the packaged binary):
    - uup-converter --input /path/to/uup_folder --output /path/to/output.iso
- Examples:
    - Convert a folder into an ISO:
        - uup-converter -i ./uup_download -o ./Windows.iso
    - Produce a WIM (if this build supports it):
        - uup-converter -i ./uup_download -w ./install.wim
- The tool expects a prepared UUP folder (files arranged by a UUP downloader). It generally does not perform downloads itself.

Notes and validation
- Behavior, available flags, and supported targets depend on the upstream uup-converter release used by this package. Run `uup-converter --help` to view supported options.
- Validate generated ISO/WIM images with your usual VM or deployment tooling before production use.

Maintainers and reporting bugs
- Packaging maintenance: see this repository for the maintainers list or top-level README.
- Report packaging issues in this repository's issue tracker. For tool-specific bugs, prefer the upstream project's issue tracker.

Tests
- No package-specific tests are included. Verify artifacts manually or with your normal CI/validation process.
