# Secure Shell (SSH) Presentation

---

## Agenda

1. Introduction to SSH
2. How SSH Works
3. Advantages of SSH
4. SSH Key Authentication
5. SSH Use Cases and Commands
6. Comparison with Telnet
7. Conclusion

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

---

## 4. SSH Key Authentication

### How SSH Keys Work

-   SSH keys consist of a public key and a private key.
-   The public key is stored on the server, and the private key is kept by the user.
-   Authentication occurs without the need for a password.

### Benefits

-   Increased security: no need to transmit passwords over the network.
-   Convenient and efficient for automated processes.

---

## 5. SSH Config File and Use Cases

### What is config file?

-   The config file is a text file that stores SSH Connection and configurations.

-   This is located in ~/.ssh/config

#### **Store connection parameters:**

-   Helps to simplify SSH connections by storing parameters such as usernames, ports and keys.

#### **Setup Alias**

-   Can use to create shprtcut names for hosts where instead of using `ssh username@123.45.67.89`
    we could use
    `ssh dev1`

#### **Manages Jump Hosts:**

-   Configure proxy commands or jump host settings

#### **Control TimeOuts:**

-   Set connection timeout and keep-alive parameters

#### **Configures authentication options:**

-   Specify which keys to use for which hosts

#### Example Config File

```bash
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 5

Host myserver
    HostName example.com
    User admin
    Port 2222


Host dev5
   HostName limedev5.linear6.com
   User ec2-user
   IdentityFile ~/.ssh/limekeys.pem
```

### **To connect to a host:**

```
ssh -i ~/.ssh/limekeys.pem ec2-user@limedev5.linear6.com
```

-   If the above configuration has been setup in the config file, it can be easily accessed using just `ssh dev5`

---

## 6. SSH Use Cases and Commands

### Common SSH Use Cases

1. **Remote Server Access:**

-   Connect to a remote server securely.

```bash
ssh username@remote-server
```

---
