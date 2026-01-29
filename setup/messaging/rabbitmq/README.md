# 🐇 RabbitMQ – Production SSL Setup

This document describes how to prepare the SSL directory structure for a **production-grade RabbitMQ setup**.

---

## 1️⃣ Create SSL Directory

```bash
sudo mkdir -p /etc/rabbitmq/ssl
cd /etc/rabbitmq/ssl
```

---

## 2️⃣ Generate CA Certificate (Root CA)

```bash
sudo openssl genrsa -out ca.key 4096
```

```bash
sudo openssl req -x509 -new -nodes -key ca.key \
-sha256 -days 3650 -out ca.pem \
-subj "/C=IN/ST=MH/L=Pune/O=KaushVerse/OU=DevOps/CN=KaushVerse-CA"
```

---

## 3️⃣ Create Server Key & CSR

```bash
sudo openssl genrsa -out server.key 4096
```

```bash
sudo openssl req -new -key server.key -out server.csr \
-subj "/C=IN/ST=MH/L=Pune/O=KaushVerse/OU=RabbitMQ/CN=<DOMAIN>"
```

---

## 4️⃣ SAN Configuration (Very Important 🔥)

```bash
sudo nano san.ext
```

Paste:

```bash
subjectAltName = DNS:<DOMAIN>,DNS:localhost,IP:127.0.0.1
```

---

## 5️⃣ Sign Server Certificate with CA

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

---

## 6️⃣ Fix Permissions ❗

```bash
sudo chown -R rabbitmq:rabbitmq /etc/rabbitmq/ssl
sudo chmod 600 /etc/rabbitmq/ssl/server.key
```

---

## 7️⃣ RabbitMQ Configuration

```bash
sudo nano /etc/rabbitmq/rabbitmq.conf
```

```conf
listeners.tcp = none

listeners.ssl.default = 5671

ssl_options.cacertfile = /etc/rabbitmq/ssl/ca.pem
ssl_options.certfile   = /etc/rabbitmq/ssl/server.pem
ssl_options.keyfile    = /etc/rabbitmq/ssl/server.key

ssl_options.verify = verify_peer
ssl_options.fail_if_no_peer_cert = false

management.tcp.port = 15672
management.tcp.ip   = 0.0.0.0

loopback_users.guest = false
```

---

## 8️⃣ Restart RabbitMQ

```bash
sudo systemctl restart rabbitmq-server
```

---

## 9️⃣ Verify SSL Listener

```bash
sudo rabbitmq-diagnostics listeners
```

Expected:

```
Interface: [::], port: 5671, protocol: amqp/ssl
```

---

# 🏠 VHost Setup

```bash
sudo rabbitmqctl add_vhost myvhost
sudo rabbitmqctl list_vhosts
```

---

# 👤 User Setup

### App User

```bash
sudo rabbitmqctl add_user app_user AppUser@456
```

### Admin User

```bash
sudo rabbitmqctl add_user admin_user Admin@123
```

```bash
sudo rabbitmqctl list_users
```

---

## 🏷️ User Tags

```bash
sudo rabbitmqctl set_user_tags app_user
sudo rabbitmqctl set_user_tags admin_user administrator
```

---

## 🔐 Permissions (MOST IMPORTANT 🔥)

### App User (myvhost only)

```bash
sudo rabbitmqctl set_permissions -p myvhost app_user ".*" ".*" ".*"
```

Remove default vhost access:

```bash
sudo rabbitmqctl clear_permissions -p / app_user
```

### Admin User (all vhosts)

```bash
sudo rabbitmqctl set_permissions -p myvhost admin_user ".*" ".*" ".*"
sudo rabbitmqctl set_permissions -p / admin_user ".*" ".*" ".*"
```

---

## 🧪 Verify Permissions

```bash
sudo rabbitmqctl list_permissions -p myvhost
```

---

## 🧨 Security Checklist

```bash
sudo rabbitmqctl delete_user guest
```

---

## 📊 Permission Order (MANDATORY)

```
configure → write → read
```

| Type      | Meaning                        |
| --------- | ------------------------------ |
| configure | queues/exchanges create/delete |
| write     | publish messages               |
| read      | consume messages               |

---

## 🛡️ Production Best Practices

* ❌ Never use `/` vhost for apps
* ✅ One app = one vhost = one user
* 🔍 Audit regularly

```bash
rabbitmqctl list_permissions
rabbitmqctl list_user_permissions app_user
```
