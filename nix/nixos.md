# Nix Package Manager — Installation Guide (Ubuntu)

> **Note:** This guide installs the **Nix package manager** on Ubuntu.
> This is different from NixOS (a full Linux distro). You get all the same
> powerful features: reproducible builds, atomic upgrades, and rollbacks.

---

## Prerequisites

- Ubuntu 18.04 or later
- `curl` installed
- `sudo` access

---

## Installation Steps

### 1. Run the official Nix installer
```bash
curl -L https://nixos.org/nix/install | sh -s -- --daemon
```

> The `--daemon` flag sets up a **multi-user installation** (recommended).
> It will ask for your sudo password during setup.

### 2. Reload your shell environment
```bash
source /etc/profile.d/nix.sh
```

Or simply close and reopen your terminal.

### 3. Verify the installation
```bash
nix --version
```

Expected output:
```
nix (Nix) 2.x.x
```

### 4. Enable Nix Flakes (recommended)

Flakes are the modern, reproducible way to manage Nix packages and projects.
```bash
mkdir -p ~/.config/nix
echo "experimental-features = nix-command flakes" >> ~/.config/nix/nix.conf
```

### 5. Test with a sample package
```bash
nix-env -iA nixpkgs.hello
hello
```

Expected output:
```
Hello, world!
```

---

## What Happens Under the Hood

When you install a package with Nix, it is placed in an isolated directory
under `/nix/store/` with a unique hash in the name. For example:
```
/nix/store/8qi947kixhz1nw83dkwxm6d0wndprqkj-hello-2.12.2
```

This design means:

- Multiple versions of the same package can coexist without conflict
- Dependencies are never shared in a way that could break other packages
- Every installation is atomic and fully reversible

---

## Basic Usage

| Task | Command |
|------|---------|
| Install a package | `nix-env -iA nixpkgs.<package>` |
| Remove a package | `nix-env -e <package>` |
| List installed packages | `nix-env -q` |
| Update all packages | `nix-env -u` |
| Roll back last change | `nix-env --rollback` |
| Open a temporary shell | `nix shell nixpkgs#<package>` |
| Search for a package | `nix search nixpkgs <query>` |

---

## Uninstalling Nix

To completely remove Nix from your system:
```bash
sudo systemctl stop nix-daemon
sudo systemctl disable nix-daemon
sudo rm -rf /nix /etc/nix /etc/profile.d/nix.sh
sudo userdel nixbld1  # repeat for nixbld1–nixbld32
```

---

## Resources

- [Official Nix Documentation](https://nixos.org/manual/nix/stable/)
- [Nixpkgs Package Search](https://search.nixos.org/packages)
- [Nix Pills (beginner guide)](https://nixos.org/guides/nix-pills/)
- [Flakes Guide](https://nixos.wiki/wiki/Flakes)
