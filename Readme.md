# uup-converter (Nix package)

This repository provides a **Nix package and flake** for **uup-converter**, a tool that converts Windows UUP (Unified Update Platform) downloads into installation media such as **ISO** or **WIM** images.

This repo focuses on **packaging**. For detailed usage, supported flags, and licensing terms, always refer to the upstream project.

---

## Upstream

* **Upstream project:** [https://git.uupdump.net/uup-dump/converter](https://git.uupdump.net/uup-dump/converter)
* **This repository:** [https://github.com/Cairnstew/uup-converter-nix](https://github.com/Cairnstew/uup-converter-nix)
* **License:** See the upstream repository for the authoritative license information

---

## Requirements

* Linux
* Nix
* A prepared UUP download directory (this tool does **not** download UUP files itself)

All runtime dependencies are provided via Nix.

---

## Usage with flakes (recommended)

### Build

```bash
nix build github:Cairnstew/uup-converter-nix
```

Or explicitly:

```bash
nix build github:Cairnstew/uup-converter-nix#uup-converter
```

### Run

```bash
nix run github:Cairnstew/uup-converter-nix -- --help
```

(The `--` separates Nix arguments from program arguments.)

---

## Building locally (non-flake / legacy)

From the repository root:

```bash
nix-build -A uup-converter
```

This creates a `./result` symlink. The binary will be available at:

```bash
./result/bin/uup-converter
```

---

## Installing

### Per-user (legacy)

```bash
nix-env -f . -iA uup-converter
```

### Declarative NixOS

Add the package to your configuration:

```nix
environment.systemPackages = [
  pkgs.uup-converter
];
```

(Or use `home-manager`’s `home.packages`.)

---

## Basic usage

Run the tool with `--help` to see the exact options supported by the packaged version:

```bash
uup-converter --help
```

Typical examples:

```bash
# Convert a UUP folder into an ISO
uup-converter -i ./uup_download -o ./Windows.iso

# Produce a WIM image (if supported by the upstream version)
uup-converter -i ./uup_download -w ./install.wim
```

The input directory must already contain a valid UUP file layout produced by a UUP downloader.

---

## Notes

* Available flags and behavior depend on the upstream `uup-converter` revision packaged here.
* Always validate generated ISOs or WIMs using a VM or your deployment tooling before production use.
* This package wraps the upstream scripts and tools; it does not modify their behavior beyond providing dependencies.

---

## Bugs and maintenance

* **Packaging issues:** file issues in this repository
* **Tool bugs or feature requests:** use the upstream project’s issue tracker

---

## Tests

No automated package tests are included. Validation is expected to be performed by running the tool and testing the generated artifacts.

---
