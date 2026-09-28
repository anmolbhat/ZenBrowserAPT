# Zen Browser APT Repository (amd64) for Debian, Ubuntu, Linux Mint & Pop!_OS

Install and auto-update [Zen Browser](https://zen-browser.app) on Debian-based Linux with plain `apt`. This is an unofficial, automatically updated `.deb` package and signed APT repository, hosted on GitHub Pages.

- **Always current:** a GitHub Actions workflow checks the official [zen-browser/desktop](https://github.com/zen-browser/desktop/releases) releases every day and publishes new versions automatically.
- **Signed repository:** `InRelease` / `Release.gpg` are GPG-signed, so `apt` verifies everything it installs.
- **Rollback friendly:** the newest version and one previous version are kept in the repo.
- **Architecture:** `amd64` (x86_64) only.

> **Unofficial.** This project repackages the official Zen Browser Linux tarball into a `.deb`. It is not affiliated with or endorsed by the Zen Browser team.

## Install

```bash
# 1. Add the signing key
sudo mkdir -p /etc/apt/keyrings
sudo curl -fsSL https://anmolbhat.github.io/ZenBrowserAPT/zen-archive-keyring.gpg \
  -o /etc/apt/keyrings/zen-archive-keyring.gpg

# 2. Add the repository
echo "deb [signed-by=/etc/apt/keyrings/zen-archive-keyring.gpg] https://anmolbhat.github.io/ZenBrowserAPT stable main" \
  | sudo tee /etc/apt/sources.list.d/zen.list

# 3. Install
sudo apt update
sudo apt install zen-browser
```

Launch it from your application menu ("Zen Browser") or run `zen-browser` in a terminal.

## Update

Updates arrive with the rest of your system packages:

```bash
sudo apt update && sudo apt upgrade
```

## Install an older version

```bash
apt policy zen-browser                     # list available versions
sudo apt install zen-browser=<version>     # e.g. zen-browser=1.22.3~beta
```

## Uninstall

```bash
sudo apt remove zen-browser
sudo rm /etc/apt/sources.list.d/zen.list /etc/apt/keyrings/zen-archive-keyring.gpg
```

## Supported systems

Any `amd64` distribution that uses `apt` and has a reasonably recent GTK 3 and glibc, including Debian 12+, Ubuntu 22.04+, Linux Mint, Pop!_OS, and Zorin OS. Other architectures (arm64, etc.) are not published.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| `NO_PUBKEY` or "not signed" during `apt update` | The key file is missing or in the wrong place. Re-run step 1 and check that `/etc/apt/keyrings/zen-archive-keyring.gpg` is not empty. |
| `Unable to locate package zen-browser` | Run `sudo apt update` after adding the source. Check that the machine is `amd64` (`dpkg --print-architecture`). |
| `apt` skips the repo with an architecture warning | The repo only provides `amd64` packages. |

## How it works

1. A scheduled GitHub Actions workflow reads the latest release from the official Zen Browser repository.
2. If the version is new, it downloads `zen.linux-x86_64.tar.xz` and builds a `.deb` (installed under `/opt/zen`, with a `zen-browser` launcher and desktop entry).
3. It generates and signs the APT metadata (`Packages`, `Release`, `InRelease`).
4. It deploys the result to GitHub Pages.

Repository layout (all served from the base URL below):

| Path | Purpose |
| --- | --- |
| `/zen-archive-keyring.gpg` | Public signing key |
| `/dists/stable/InRelease` | Signed release index |
| `/dists/stable/Release`, `/dists/stable/Release.gpg` | Release index and detached signature |
| `/dists/stable/main/binary-amd64/Packages` | Package list |
| `/pool/main/` | The `.deb` files |
| `/VERSION` | Currently published Zen version |

Base URL: `https://anmolbhat.github.io/ZenBrowserAPT`

## FAQ

**Is this the official Zen Browser package?** No. The binaries come from the official releases; only the packaging and hosting are done here.

**Why isn't there a Flatpak or AppImage?** Zen provides those upstream. This repo exists for people who want native `apt` installs and automatic updates.

**Where do I report problems with the browser itself?** At [zen-browser/desktop](https://github.com/zen-browser/desktop/issues). Packaging problems (install, signing, repo) go in this repo's issues.

## License

Repository scripts and workflow: GPL-3.0 (see [LICENSE](LICENSE)). Zen Browser is distributed under its own license by its authors.
