# ☁️ AWS EC2 Connection Guide

This guide explains how to connect to AWS EC2 instances in different scenarios.

---

# Scenario 1: Public EC2 Instance (Without Key Pair)

If you already have access to a public EC2 instance without using a key pair, switch to the root user.

```bash
sudo su -
```

Now you can install packages, configure services, and manage the server as the root user.

---

# Scenario 2: Public EC2 Instance (Using a Key Pair)

If your EC2 instance was created with a key pair, connect using SSH.

```bash
ssh -i key.pem ec2-user@<PUBLIC-IP>
```

Example:

```bash
ssh -i my-key.pem ec2-user@54.123.45.67
```

After connecting, switch to the root user.

```bash
sudo su -
```

---

# Give Permission to Key File

If you get a permission error, change the key file permission.

```bash
chmod 400 key.pem
```

Then connect again.

```bash
ssh -i key.pem ec2-user@<PUBLIC-IP>
```

---

# Scenario 3: Connect to a Private EC2 Instance

A private EC2 instance cannot be accessed directly from the Internet.

First connect to the Public EC2 (Bastion Host).

```bash
ssh -i key.pem ec2-user@<PUBLIC-IP>
```

Switch to the root user.

```bash
sudo su -
```

---

# Copy the Key File to the Public EC2 (Optional)

If the key file is not already on the Bastion Host, copy it from your local machine.

```bash
scp -i key.pem key.pem ec2-user@<PUBLIC-IP>:/home/ec2-user/
```

On the Public EC2:

```bash
chmod 400 key.pem
```

---

# Connect from Public EC2 to Private EC2

```bash
ssh -i key.pem ec2-user@<PRIVATE-IP>
```

Example:

```bash
ssh -i key.pem ec2-user@10.0.1.25
```

Now you are connected to the Private EC2 instance.

---

# Connection Flow

```text
Your Laptop
      │
      ▼
Public EC2 (Bastion Host)
      │
      ▼
Private EC2
```

---

# Common SSH Commands

### Connect to Public EC2

```bash
ssh -i key.pem ec2-user@<PUBLIC-IP>
```

### Connect to Private EC2

```bash
ssh -i key.pem ec2-user@<PRIVATE-IP>
```

### Switch to Root User

```bash
sudo su -
```

### Change Key Permission

```bash
chmod 400 key.pem
```

### Copy File to EC2

```bash
scp -i key.pem file.txt ec2-user@<PUBLIC-IP>:/home/ec2-user/
```

### Exit from Server

```bash
exit
```

---

# Notes

- Keep your **key.pem** file safe.
- Never share your private key with anyone.
- Use `chmod 400 key.pem` before connecting if required.
- A Private EC2 instance is not directly accessible from the Internet.
- Always connect to the Public EC2 (Bastion Host) first, then connect to the Private EC2.

---

## 👨‍💻 Author

**Ajay Patel**

**DevOps | AWS | Docker | Jenkins | Terraform | Git | Linux**
