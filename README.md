# Remote SSH Access Setup for VS Code through Jump Host

This guide explains how to set up **VS Code** to access a remote server (**Server B**) through another intermediate server (**Server A**) using **SSH Agent Forwarding** and the **Remote-SSH** extension.

## Prerequisites

- **VS Code** installed on your local machine.
- **SSH keys** set up for authentication (optional but recommended for security).
- **Remote-SSH** extension installed in VS Code.
- Access to **Server A** via SSH from your local machine.
- Access to **Server B** from **Server A** via SSH.
  
### 1. Install VS Code and the Remote-SSH Extension

- Download and install **VS Code** from [here](https://code.visualstudio.com/).
- Install the **Remote-SSH** extension:
  1. Open **VS Code**.
  2. Go to **Extensions** (click the Extensions icon on the left bar or press `Ctrl+Shift+X`).
  3. Search for "Remote - SSH" and click **Install**.

### 2. Set Up SSH Configuration

You will need to configure your SSH setup to allow a **jump host** (Server A) to forward your SSH connection to **Server B**.

#### 2.1. Edit the SSH Config on Your Local Machine

- Open or create the `~/.ssh/config` file on your **local machine**.
- Add the following configuration for **Server A**:

  ```bash
  Host serverA
    HostName serverA.com        # Replace with the actual domain or IP of Server A
    User userA                  # Replace with your username for Server A
    IdentityFile ~/.ssh/id_rsa  # Replace with your private SSH key if using key-based auth
    ForwardAgent yes            # Enable SSH agent forwarding
  
  Host serverA
      HostName serverB.com
      User userA
      ProxyJump userA@serverA.com
  ```
  ##### Now in VS-Code open command Palette (Ctrl+Shift+P) and Type:
    ```bash
      Remote-SSH: Connect to Host...
    ```
    - From the list select Server B.
