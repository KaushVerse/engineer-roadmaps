# 🐇 RabbitMQ – Production SSL Setup

This document describes how to prepare the SSL directory structure for a **production-grade RabbitMQ setup**.

---

## 1️⃣ Create SSL Directory

```bash
sudo mkdir -p /etc/rabbitmq/ssl
```

```bash
cd /etc/rabbitmq/ssl
```
## 2️⃣ CA Certificate Generate Karo (Root CA)

```bash
sudo openssl genrsa -out ca.key 4096
```
```bash
sudo openssl req -x509 -new -nodes -key ca.key \
-sha256 -days 3650 -out ca.pem \
-subj "/C=IN/ST=MH/L=Pune/O=KaushVerse/OU=DevOps/CN=KaushVerse-CA"
```