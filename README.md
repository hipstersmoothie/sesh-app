# Sesh

Sesh is a native client for coding agents on your own machines. Agents run on a host, keep working while your laptop is closed, and you check in from the Mac app.

This repository hosts **releases of the Sesh host daemon** (`seshd`) and its command-line tool (`sesh`), plus the Homebrew formula. The source isn't published here.

## Install a host

On any Mac or Linux machine you want agents to run on:

```sh
curl -fsSL https://github.com/hipstersmoothie/sesh-app/releases/latest/download/install.sh | sh
```

This installs `seshd` and `sesh` to `~/.local/bin`, starts `seshd` as a service (launchd on macOS, a systemd user unit on Linux) and prints a pairing code. Then, in the Sesh app, go to **Settings → Machines → Add Machine…**. To update a host, run the installer again or `seshd update`; the app can also update it.

Linux builds are static and run on any distribution (x86_64 and arm64).

Options, set as environment variables:

| Variable | Default | |
|---|---|---|
| `SESH_LISTEN` | `0.0.0.0` | Address to listen on |
| `SESH_INSTALL_DIR` | `~/.local/bin` | Where the binaries go |
| `SESH_NO_SERVICE=1` | | Install the binaries only |

Devices must pair with a one-time code before they can connect. Connections are encrypted (TLS with the host's own certificate, which pairing pins), so any network works; use a VPN such as Tailscale to reach the host from outside its network.

## Homebrew

```sh
brew tap hipstersmoothie/sesh https://github.com/hipstersmoothie/sesh-app
brew install sesh
```

`brew services start sesh` serves this machine only. To let other devices connect, run `seshd install --host 0.0.0.0`, then `sesh pair`.

## What a host needs

- **git**
- **Node.js 18+**: Claude Code runs through `npx`.
- **Claude Code, logged in**: `claude auth login`, or **Log In…** in the app's machine details.
- **Your project's tools**: whatever the agent needs to build and test.

`sesh info` on the host shows what's installed and logged in.
