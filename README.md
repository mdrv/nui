# nui

**nui** is short for **nu installation** — install prebuilt
[Nushell](https://www.nushell.sh) on macOS & Linux in one command. No
compiler, no Homebrew, no waiting on a source build.

```sh
curl -fsSL https://raw.githubusercontent.com/mdrv/nui/main/nui.sh | sh
```

## What it does

1. Detects your OS and architecture (Apple silicon / Intel / ARM)
2. Resolves the latest Nushell release from GitHub (or the one you pin)
3. Downloads the official release tarball and **verifies its sha256** against
   GitHub's asset digest
4. Installs `nu` and the bundled `nu_plugin_*` binaries into `~/.local/bin`
5. Offers to add `~/.local/bin` to your `PATH` in `~/.zshrc` or `~/.bashrc`
   (asks first; when piped non-interactively it just prints the line to add)

On Linux it picks the **gnu** (glibc) build automatically, or the **musl**
build on Alpine and other musl-based distros.

## Supported platforms

| OS | Architectures |
| --- | --- |
| macOS (Darwin) | Apple silicon (`arm64`), Intel (`x86_64`) |
| Linux | `x86_64`, `aarch64` (gnu & musl), `armv7` (gnu & musl) |

## Options

| Flag | Effect |
| --- | --- |
| `--version X.Y.Z` | install a specific release instead of latest |
| `--prefix DIR` | install under `DIR/bin` (default `~/.local`) |
| `--no-path` | skip the shell-rc `PATH` offer |
| `-h, --help` | show help |

Environment equivalents: `NU_VERSION`, `NU_PREFIX`.

```sh
# examples
sh nui.sh --version 0.116.0
NU_PREFIX="$HOME/.nushell" sh nui.sh
```

## Requirements

- macOS or Linux
- `curl` and `tar` (ship with the OS on macOS, present on nearly every distro)
- one of `sha256sum`, `shasum`, or `openssl` for checksum verification
  (if none exists, the script skips verification with a warning)

## Uninstall / upgrade

```sh
# upgrade: just run the script again
# uninstall:
rm ~/.local/bin/nu ~/.local/bin/nu_plugin_*
```

## Other platforms

- **Windows**: `winget install Nushell.Nushell` (or `scoop install nushell`)
