# Sesh

Sesh is a native client for coding agents on your own machines. Agents run on a host, keep working while your laptop is closed, and you check in from the Mac app.

This repository hosts **releases of the Sesh host daemon** (`seshd`) and its command-line tool (`sesh`), plus the Homebrew formula. The source isn't published here.

## Install a host

On any Mac or Linux machine you want agents to run on:

```sh
curl -fsSL https://sesh.codes/install.sh | sh
```

This installs `seshd` and `sesh` to `~/.local/bin`, starts `seshd` as a service (launchd on macOS, a systemd user unit on Linux) and prints a pairing code. Then, in the Sesh app, go to **Settings → Machines → Add Machine…**. To update a host, run the installer again or `seshd update`; the app can also update it.

Linux builds are static and run on any distribution (x86_64 and arm64).

Options, set as environment variables:

| Variable | Default | |
|---|---|---|
| `SESH_INSTALL_DIR` | `~/.local/bin` | Where the binaries go |
| `SESH_NO_SERVICE=1` | | Install the binaries only |

Devices must pair with a one-time code before they can connect. They reach the host by its ID over iroh, end-to-end encrypted, from any network: nothing to open, forward or set up.

## Homebrew

```sh
brew tap sesh/tap https://sesh.codes/tap
brew install sesh/tap/sesh
```

After `brew services start sesh/tap/sesh`, run `sesh pair` to pair your other devices.

## What a host needs

- **git**
- **Node.js 18+**: Claude Code runs through `npx`.
- **Claude Code, logged in**: `claude auth login`, or **Log In…** in the app's machine details.
- **Your project's tools**: whatever the agent needs to build and test.

`sesh info` on the host shows what's installed and logged in.
