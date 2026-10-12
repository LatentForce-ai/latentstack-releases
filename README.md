# LatentStack releases

Downloadable builds of LatentStack: the **latentcode** CLI, the **LatentWork**
desktop app, the **LatentCode** extension for VS Code-family editors, and the
native skills bundle.

This repository holds release files only, no source code. Each version is one
[GitHub Release](https://github.com/LatentForce-ai/latentstack-releases/releases),
and the newest one is marked **Latest**.

## Install

The install scripts pick the right build for your machine and set everything up.

**macOS / Linux**

```sh
curl -fsSL https://latentstack.dev/install.sh | bash
```

**Windows (PowerShell)**

```powershell
irm https://latentstack.dev/install.ps1 | iex
```

This installs the latentcode CLI, the LatentWork desktop app, the editor
extension (into any local VS Code, VS Code Insiders, VSCodium, Cursor, Windsurf
or code-server), and the skills bundle.

| To install only… | macOS / Linux | Windows |
|---|---|---|
| the CLI | `… \| bash -s -- --cli-only` | `& ([scriptblock]::Create((irm https://latentstack.dev/install.ps1))) -CliOnly` |
| the desktop app | `… \| bash -s -- --desktop-only` | `& ([scriptblock]::Create((irm https://latentstack.dev/install.ps1))) -DesktopOnly` |
| everything except the editor extension | `… \| bash -s -- --no-vscode` | `& ([scriptblock]::Create((irm https://latentstack.dev/install.ps1))) -NoVscode` |

If your organisation runs its own LatentStack server, use that server's address
instead of `latentstack.dev`. It serves the same scripts.

The editor extension can only be installed into a local editor. For VS Code
Remote (SSH, WSL, containers), install the `.vsix` from inside the remote
session.

## Manual downloads

Every release has these files. `<version>` is the release version, for example
`0.0.42`.

### latentcode CLI

A single self-contained executable; Node and npm are not needed.

| Platform | File |
|---|---|
| macOS, Apple Silicon | `latentcode-darwin-arm64-<version>` |
| macOS, Intel | `latentcode-darwin-x64-<version>` |
| Linux x64 | `latentcode-linux-x64-<version>` |
| Linux arm64 | `latentcode-linux-arm64-<version>` |
| Linux x64, Alpine / musl | `latentcode-linux-x64-musl-<version>` |
| Linux arm64, Alpine / musl | `latentcode-linux-arm64-musl-<version>` |
| Windows x64 | `latentcode-windows-x64-<version>.exe` |
| Windows arm64 | `latentcode-windows-arm64-<version>.exe` |

**`-baseline` builds** (`darwin-x64-baseline`, `linux-x64-baseline`,
`linux-x64-baseline-musl`, `windows-x64-baseline`) are for older x64 CPUs
without AVX2. Use one if the normal build exits with "illegal instruction".

**`latentcode-natives-<platform>-<version>.tar.gz`** adds code-search and
code-edit support (`ast_grep` / `ast_edit`). Extract it into the same folder as
the `latentcode` binary. The CLI runs without it, just without those two tools.

On macOS and Linux, make the binary executable after downloading:

```sh
chmod +x latentcode-*
```

### LatentWork desktop app

| Platform | File |
|---|---|
| macOS, Apple Silicon | `latentwork-mac-arm64-<version>.dmg` |
| Windows x64 | `latentwork-win-x64-<version>.exe` (installer) |
| Linux x64 | `latentwork-linux-x86_64-<version>.AppImage` |
| Linux x64, portable | `latentwork-linux-x64-<version>.tar.gz` |

The app updates itself once installed. The `latest*.yml` files and the macOS
`.zip` exist for that updater; you don't need to download them.

On Linux, make the AppImage executable before running it:
`chmod +x latentwork-*.AppImage`.

### Editor extension

`latentcode-vscode-<version>.vsix` is one file for every platform. Install it
from the command line:

```sh
code --install-extension latentcode-vscode-<version>.vsix
```

or from the editor: Extensions → `…` menu → **Install from VSIX…**

### Skills bundle

`latentstack-plugins-skills-<version>.tar.gz` holds the built-in skills. The
install script puts them in `~/.latentcode/plugins/skills/` and checks the
file's SHA-256 against the one listed in `manifest.json`.

## Versions

- One version number covers every product in a release: the CLI, the
  extension, the skills and LatentWork all share it.
- Tags are `v<version>`, for example `v0.0.42`.
- A published release is never changed or replaced. A fix ships as a new
  version.
- File names include the version, so a direct link always points at one exact
  build.