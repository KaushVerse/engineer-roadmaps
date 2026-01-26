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

## 3️⃣ Server Key & CSR Banao

```bash
sudo openssl genrsa -out server.key 4096
```
```bash
sudo openssl req -new -key server.key -out server.csr \
-subj "/C=IN/ST=MH/L=Pune/O=KaushVerse/OU=RabbitMQ/CN=[rmq.kaushverse.com](http://rmq.kaushverse.com/)"
```

## 4️⃣ SAN (Very Important 🔥)

```bash
sudo nano san.ext
```
#### paste:

```bash
subjectAltName = DNS:rmq.kaushverse.com,DNS:localhost,IP:127.0.0.1
```

## 5️⃣ Server Certificate Sign Karo (CA se)

```bash
sudo openssl x509 -req \
-in server.csr \
-CA ca.pem \
-CAkey ca.key \
-CAcreateserial \
-out server.pem \
-days 365 \
-sha256 \
-extfile san.ext
```