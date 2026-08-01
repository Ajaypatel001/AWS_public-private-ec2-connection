# ☁️ AWS EC2 Connection Guide

This guide explains how to connect AWS EC2 instances in different scenarios.

---

# Scenario 1: Public EC2 (Without Key Pair)

If the EC2 instance is already accessible, switch to the root user.

```bash
sudo su -
```

---

# Scenario 2: Public EC2 (Using Key Pair)

Create a key file.

```bash
vi key.pem
```

Paste the complete private key inside the file.

Press:

```text
Esc
:wq!
```

Change the file permission.

```bash
chmod 400 key.pem
```

Connect to the Public EC2.

```bash
ssh -i key.pem ec2-user@<PUBLIC-IP>
```

Example:

```bash
ssh -i key.pem ec2-user@54.xxx.xxx.xxx
```

After login:

```bash
sudo su -
```

---

# Scenario 3: Connect to Private EC2 Using Bastion Host

A Private EC2 cannot be accessed directly from the Internet.

### Step 1: Login to Public EC2 (Bastion Host)

```bash
vi key.pem
```

Paste the private key.

Save the file.

```text
Esc
:wq!
```

Give permission.

```bash
chmod 400 key.pem
```

Connect to the Public EC2.

```bash
ssh -i key.pem ec2-user@<PUBLIC-IP>
```

Switch to root.

```bash
sudo su -
```

---

### Step 2: Create Key Again (If Required)

If the key file is not available after switching servers, create it again.

```bash
vi key.pem
```

Paste the private key.

Save.

```text
Esc
:wq!
```

Give permission.

```bash
chmod 400 key.pem
```

---

### Step 3: Connect to Private EC2

```bash
ssh -i key.pem ec2-user@<PRIVATE-IP>
```

Example:

```bash
ssh -i key.pem ec2-user@10.0.1.25
```

After login:

```bash
sudo su -
```

---

# Scenario 4: Frontend EC2 + Backend EC2

Architecture

```text
                Internet
                     │
                     ▼
        Frontend EC2 (Public)
              Bastion Host
                     │
                     ▼
         Backend EC2 (Private)
```

### Connect to Frontend

```bash
vi key.pem
```

Paste the private key.

Save.

```text
Esc
:wq!
```

Permission.

```bash
chmod 400 key.pem
```

Login.

```bash
ssh -i key.pem ec2-user@<FRONTEND_PUBLIC_IP>
```

Become root.

```bash
sudo su -
```

---

### Connect Frontend to Backend

Again create the key if required.

```bash
vi key.pem
```

Paste the key.

Save.

```text
Esc
:wq!
```

Permission.

```bash
chmod 400 key.pem
```

Connect to Backend.

```bash
ssh -i key.pem ec2-user@<BACKEND_PRIVATE_IP>
```

Become root.

```bash
sudo su -
```

---

# Connection Flow

```text
Laptop
   │
   ▼
vi key.pem
   │
Paste Key
   │
:wq!
   │
chmod 400 key.pem
   │
ssh -i key.pem ec2-user@Public-IP
   │
sudo su -
   │
vi key.pem
   │
Paste Key
   │
:wq!
   │
chmod 400 key.pem
   │
ssh -i key.pem ec2-user@Private-IP
   │
sudo su -
```

---

# Commands Summary

```bash
vi key.pem
chmod 400 key.pem
ssh -i key.pem ec2-user@<PUBLIC-IP>
ssh -i key.pem ec2-user@<PRIVATE-IP>
sudo su -
exit
```

---

## 👨‍💻 Author

**Ajay Patel**

**DevOps | AWS | Docker | Jenkins | Terraform | Git | Linux**
