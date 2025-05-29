# Fedora 42 on Windows WSL: Quick Start Guide

This guide will help you set up Fedora on Windows Subsystem for Linux (WSL), install essential tools, and configure fractional scaling for graphical sessions.

## References

* [Fedora WSL Documentation](https://docs.fedoraproject.org/en-US/cloud/wsl/)
* [Microsoft WSL Basic Commands](https://learn.microsoft.com/en-us/windows/wsl/basic-commands)
* [Fedora: Running Waypipe on Microsoft Windows?](https://discussion.fedoraproject.org/t/running-waypipe-on-microsoft-windows/128977/2)
* [Red Hat: Remotely Accessing a Wayland-based Application](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/getting_started_with_the_gnome_desktop_environment/remotely-accessing-an-individual-application-wayland_getting-started-with-the-gnome-desktop-environment)

---

## 1. Install WSL

Open **PowerShell** with Administrator rights and run:

```powershell
wsl --install --no-distribution
```

## 2. Reboot Your Machine

Run the following command in PowerShell to reboot immediately:

```powershell
shutdown.exe /r /t 0
```

## 3. List Available Distributions

After rebooting, list available WSL distributions:

```powershell
wsl --list --online
```

## 4. Install Fedora

To install Fedora (for example, Fedora Linux 42):

```powershell
wsl --install -d FedoraLinux-42
```

## 5. Install Useful Tools

Once Fedora is installed and running, install useful tools by running:

```bash
sudo sed -i '/^\[main\]$/a max_parallel_downloads=20' /etc/dnf/dnf.conf

sudo dnf install -y vim-enhanced nano bat git wget curl axel zstd bash-completion ncdu btop htop nmon tmux fuse-sshfs waypipe
```

### 5.1 Set Up an SSH Key for the Current User

```bash
ssh-keygen -t ed25519 -a 100 -N "" -f ~/.ssh/id_ed25519 -q
```

### 5.2 Fix Fractional Scaling for Waypipe (If Needed)

If fractional scaling is not working, add the following workaround:

```bash
tee ~/.wlsgconfig > /dev/null << EOF
[system-distro-env]
WESTON_RDP_DISABLE_FRACTIONAL_HI_DPI_SCALING=false
WESTON_RDP_DEBUG_DESKTOP_SCALING_FACTOR=175
EOF
```

## 6. Reboot or Close All Running WSL Instances if Waypipe still has issues

```powershell
wsl --shutdown
```
