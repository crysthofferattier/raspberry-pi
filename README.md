
# 🛠 Raspberry Pi Setup Guide (Dev Environment with SSH, Docker, and VSCode)

---

### 🔄 Update & Upgrade System

Always start by updating your system to the latest packages for security and compatibility.

```bash
sudo apt update        # Refresh package lists
sudo apt upgrade -y    # Install available upgrades without prompt
```

---

### 🔐 SSH Configuration

Generate an SSH key and set up secure, passwordless authentication.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
# Generates a new Ed25519 key pair.
# This is more secure and efficient than RSA.
# The email is optional metadata.

mkdir -p ~/.ssh
# Ensures the .ssh directory exists

touch ~/.ssh/authorized_keys
# Creates the file that stores allowed public keys

chmod 700 ~/.ssh
# Restricts access to the .ssh folder (owner only)

chmod 600 ~/.ssh/authorized_keys
# Restricts access to the authorized_keys file (read/write for owner only)
```

> ✅ After this, you can copy your public key (`~/.ssh/id_ed25519.pub`) to any server's `~/.ssh/authorized_keys` to enable SSH login without a password.

---

### 🐳 Docker Installation

Install Docker using the official convenience script.

```bash
curl -sSL https://get.docker.com | sh
# Downloads and installs the latest Docker Engine for your architecture
```

**Alternative: download script separately (useful for audit or offline use):**

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
# Saves the script locally
sudo sh get-docker.sh
# Executes the script
```

Enable Docker to start on boot:

```bash
sudo systemctl enable docker
# Ensures Docker service starts automatically on system boot
```

Add your user to the `docker` group:

```bash
sudo usermod -aG docker $USER
# Allows running docker commands without sudo

newgrp docker
# Refresh group membership for the current session

sudo reboot
# Reboot to apply changes (recommended)

docker --version
# Verify Docker is installed correctly
```

✅ Test Docker with:

```bash
docker run hello-world
# Pulls and runs a test container to confirm installation
```

---

### 🖥️ Visual Studio Code (VSCode)

Install VSCode on your Raspberry Pi.

> ⚠️ **Download the ARM `.deb` version** from the official site:
> [Download VS Code](https://code.visualstudio.com/download)

* Choose `.deb` for ARM architecture (Raspberry Pi OS is ARM-based).
* Install with `sudo dpkg -i code-xxx.deb` if needed.

---

#### 📦 Recommended Extensions

These extensions improve your development workflow for Python, Docker, and remote development:

1. [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) — Python language support.
2. [Black Formatter](https://marketplace.visualstudio.com/items?itemName=ms-python.black-formatter) — Code formatter for clean Python code.
3. [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) — Enables editing remote files over SSH.
4. [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) — Manage containers and images from within VSCode.

Install extensions from the terminal:

```bash
code --install-extension ms-python.python
code --install-extension ms-python.black-formatter
code --install-extension ms-vscode-remote.remote-ssh
code --install-extension ms-azuretools.vscode-docker
```

---