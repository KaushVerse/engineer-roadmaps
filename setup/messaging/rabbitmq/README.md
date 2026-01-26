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
-subj "/C=IN/ST=MH/L=Pune/O=KaushVerse/OU=RabbitMQ/CN=[<DOMAIN>](http://<DOMAIN>/)"
```

## 4️⃣ SAN (Very Important 🔥)

```bash
sudo nano san.ext
```
#### paste:

```bash
subjectAltName = DNS:<DOMAIN>,DNS:localhost,IP:127.0.0.1
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

## 6️⃣ Permission Fix (Important ❗)

```bash
sudo chown -R rabbitmq:rabbitmq /etc/rabbitmq/ssl
```
```bash
sudo chmod 600 /etc/rabbitmq/ssl/server.key
```

## 7️⃣ rabbitmq.conf Edit Karo (nano path)

```bash
sudo nano /etc/rabbitmq/rabbitmq.conf
```

## 🔐 AMQPS Enable (5671)
### Disable plain AMQP (optional but recommended)

```bash
listeners.tcp = none

## Enable SSL listener

listeners.ssl.default = 5671

ssl_options.cacertfile = /etc/rabbitmq/ssl/ca.pem
ssl_options.certfile   = /etc/rabbitmq/ssl/server.pem
ssl_options.keyfile    = /etc/rabbitmq/ssl/server.key

ssl_options.verify = verify_peer
ssl_options.fail_if_no_peer_cert = false

## Management UI (HTTP)

management.tcp.port = 15672
management.tcp.ip   = 0.0.0.0

loopback_users.guest = false
```

## 8️⃣ Restart RabbitMQ

```bash
sudo systemctl restart rabbitmq-server
```

## 9️⃣ Verify Listeners ✅

```bash
sudo rabbitmq-diagnostics listeners
```

#### Expected Output:
##### Interface: [::], port: 5671, protocol: amqp/ssl


# 🏠 Step 1: VHost create karo (myvhost)

```bash
sudo rabbitmqctl add_vhost myvhost
```
#### Verify:

```bash
sudo rabbitmqctl list_vhosts
```