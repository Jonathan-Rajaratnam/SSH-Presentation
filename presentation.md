# Secure Shell (SSH) Presentation

---

## Agenda

1. Introduction to SSH
2. How SSH Works
3. Advantages of SSH
4. SSH Key Authentication
5. SSH Config File and Use Cases
6. Setting Up SSH
7. Telnet

---

## 1. Introduction to SSH

### What is SSH?

SSH, or Secure Shell, is a cryptographic network protocol used for secure communication over an unsecured network. It provides a secure channel over an insecure network, such as the internet.

### Key Features

-   Encrypted communication
-   Authentication
-   Secure file transfer (SCP and SFTP)
-   Tunneling for secure network services

---

## 2. How SSH Works

1. **Encryption:** SSH encrypts data during transmission to prevent eavesdropping.
2. **Authentication:** Users must authenticate using a username and password or SSH keys.
3. **Secure Connection:** SSH creates a secure connection between the client and server.

---

## 3. Advantages of SSH

### Security

-   Encrypts data to prevent unauthorized access.
-   Protects against eavesdropping and man-in-the-middle attacks.

### Authentication

-   Supports password-based authentication and public-key cryptography.
-   Two-factor authentication can be implemented for added security.

### Remote Access

-   Allows users to access remote servers securely.
-   Widely used for remote administration of servers.

### Flexibility

-   Can tunnel other protocols through SSH connections.
-   Supports port forwarding and SOCKS proxying.

### Wide Support

-   Built into most operating systems (Linux, macOS).
-   Available for Windows through various clients.
-   Industry standard with extensive documentation.

### Efficiency

-   Connection sharing allows multiple sessions over a single connection.
-   Compression options for improved performance over slow networks.

---

## 4. SSH Key Authentication

### How SSH Keys Work

-   SSH keys consist of a public key and a private key.

-   The public key is stored on the server, and the private key is kept by the user.

-   Authentication occurs without the need for a password.

-   Keys use asymmetric encryption (typically RSA, Ed25519, or ECDSA).

### Key Generation

-   Created using `ssh-keygen` command:

    ```bash
    ssh-keygen -t ed25519 -C "your_email@example.com"
    ```

-   Keys are typically stored in the ~/.ssh directory.

### Benefits

-   Increased security: No need to transmit passwords over the network.

-   Convenient and efficient for automated processes.

-   Protection against brute force attacks.

-   Single key can be used across multiple servers.

-   Can implement passphrase protection for additional security.

### Best Practices

-   Keep private keys secure and never share them.

-   Use strong passphrases for private keys.

-   Consider using ssh-agent to manage passphrases.

-   Regularly audit and rotate keys when necessary.

---

## 5. SSH Config File and Use Cases

### What is config file?

-   The config file is a text file that stores SSH Connection and configurations.

-   This is located in ~/.ssh/config

#### **Store connection parameters:**

-   Helps to simplify SSH connections by storing parameters such as usernames, ports and keys.

#### **Setup Alias**

-   Can use to create shortcut names for hosts where instead of using
    `ssh username@123.45.67.89`
    we could use
    `ssh dev1`

#### **Manages Jump Hosts:**

-   Configure proxy commands or jump host settings

#### **Control TimeOuts:**

-   Set connection timeout and keep-alive parameters

#### **Configures authentication options:**

-   Specify which keys to use for which hosts

---

### Example Config File

```bash
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 5

Host myserver
    HostName example.com
    User admin
    Port 2222


Host dev3
   HostName limedev3.linear6.com
   User ec2-user
   IdentityFile ~/.ssh/limekeys.pem
```

### **To connect to a host:**

```
ssh -i ~/.ssh/limekeys.pem ec2-user@limedev5.linear6.com
```

-   If the above configuration has been setup in the config file, it can be easily accessed using just `ssh dev5`

---

## 6. Setting Up SSH

### 1. **Check For SSH Folder**

-   Check if .ssh folder exists in home directory.

-   Open Terminal and try `cd .ssh`

-   If Folder doesn't exist then create it with `mkdir .ssh` and then `cd .ssh`

### 2. Creating Config File

-   Using any text editor of choice or using vscode `code .`

-   Create a new file as `config`

-   Copy the host configurations

-   Make sure that the key files are present `limekeys.pem`

### 3. Test Connection

-   We can test our ssh connection using full ssh method

    -   `ssh -t -i ~/.ssh/limekeys.pem ec2-user@limedev3.linear6.com`

-   Using config file alias

    -   `ssh dev3`

---

## 7. Other Uses of SSH

### **Secure File Transfers:**

-   **SCP (Secure Copy) for simple file transfers**

    -   SCP: Copy a file to a remote server

    `scp document.pdf user@remote-server:/home/user/documents/`

    -   SCP: Copy a directory recursively from a remote server

    `scp -r user@remote-server:/var/www/backup/ ./local-backup/`

-   **SFTP (SSH File Transfer Protocol) for more interactive file management**
    <br>
    <br>

    -   SFTP: Interactive file management
        <br>
        <br>

        ```bash
        sftp user@remote-server
        > cd /var/www
        > ls -la
        > get important-file.txt
        > put local-file.txt
        > bye
        >
        ```

-   **Rsync over SSH for efficient file synchronization and backups**

### **Remote Code Execution:**

-   **Running commands on remote servers without logging in**
-   **Executing scripts across multiple servers simultaneously**
    <br>
    <br>
    `ssh user@remote-server "ls -la /var/log"`
    <br>
    <br>
    `ssh user@remote-server "cat /var/log/log.txt"`
    <br>
    <br>

---

### **Git Operations:**

-   **Secure authentication for GitHub, GitLab, and other repositories**

    -   Clone a repository using SSH. This will be the preferred method when cloning our bitbucket repos
        <br>
        <br>

    `git clone git@github.com:username/repository.git`
    <br>
    <br>

-   **Push/pull operations without password prompts**

### **X11 Forwarding:**

-   Running graphical applications from remote machines

-   Displaying GUI interfaces locally from remote applications
    <br>
    <br>
    ` ssh -X user@remote-server xclock`

---

### **VPN Alternative:**

-   **Creating encrypted tunnels for secure browsing**
-   **Accessing internal networks securely from external locations**

### **Port Forwarding:**

-   **Local forwarding to access remote services securely**

    -   Local forwarding: Access a remote MySQL server locally
        <br>
        <br>
        `ssh -L 3306:localhost:3306 user@remote-server`
        <br>
        <br>

-   **Remote forwarding to expose local services to remote machines**
-   **Dynamic forwarding to create a SOCKS proxy**

### **Jump Hosts / Bastion Servers:**

-   Using intermediate servers to access protected networks
-   Controlling access to infrastructure through a single point

---

## 8. Telnet Overview

Telnet is one of the earliest remote login protocols, developed in 1969 as part of the ARPANET project. It stands for "TELecommunication NETwork" and provides a text-based interface for interacting with remote computers.

### Key Points About Telnet:

-   Transmits all data (including usernames and passwords) in plaintext
-   Operates on TCP port 23 by default
-   No built-in encryption or strong authentication mechanisms
-   Was widely used before security became a major concern
-   Still used occasionally for specific networking diagnostics and internal/isolated networks
-   Now considered insecure for most modern applications

## Telnet vs SSH Comparison

<table>
  <tr>
    <th>Feature</th>
    <th>SSH</th>
    <th>Telnet</th>
  </tr>
  <tr>
    <td><strong>Encryption</strong></td>
    <td>All communications encrypted</td>
    <td>No encryption (plaintext)</td>
  </tr>
  <tr>
    <td><strong>Authentication</strong></td>
    <td>Password, public key, certificates, 2FA</td>
    <td>Basic password authentication (sent in plaintext)</td>
  </tr>
  <tr>
    <td><strong>Data Integrity</strong></td>
    <td>Ensures data integrity</td>
    <td>No data integrity verification</td>
  </tr>
  <tr>
    <td><strong>Default Port</strong></td>
    <td>22/TCP</td>
    <td>23/TCP</td>
  </tr>
  <tr>
    <td><strong>Security</strong></td>
    <td>High</td>
    <td>Very low</td>
  </tr>
  <tr>
    <td><strong>Commands</strong></td>
    <td><code>ssh user@host</code></td>
    <td><code>telnet host</code></td>
  </tr>
  <tr>
    <td><strong>File Transfer</strong></td>
    <td>Built-in (SCP, SFTP)</td>
    <td>Not available natively</td>
  </tr>
  <tr>
    <td><strong>Port Forwarding</strong></td>
    <td>Supported</td>
    <td>Not supported</td>
  </tr>
  <tr>
    <td><strong>Modern Usage</strong></td>
    <td>Industry standard</td>
    <td>Legacy systems only</td>
  </tr>
  <tr>
    <td><strong>Year Introduced</strong></td>
    <td>1995</td>
    <td>1969</td>
  </tr>
  <tr>
    <td><strong>Protocol</strong></td>
    <td>Application layer</td>
    <td>Application layer</td>
  </tr>
  <tr>
    <td><strong>Standardization</strong></td>
    <td>RFC 4251-4254</td>
    <td>RFC 854</td>
  </tr>
  <tr>
    <td><strong>Connection Maintenance</strong></td>
    <td>Robust, with keep-alive options</td>
    <td>Basic, prone to timeouts</td>
  </tr>
  <tr>
    <td><strong>Additional Features</strong></td>
    <td>X11 forwarding, agent forwarding, tunneling</td>
    <td>Basic terminal emulation only</td>
  </tr>
  <tr>
    <td><strong>Cross-platform Support</strong></td>
    <td>Excellent</td>
    <td>Limited in modern systems</td>
  </tr>
</table>
