# 🐇 RabbitMQ – Production SSL Setup

This document describes how to prepare the SSL directory structure for a **production-grade RabbitMQ setup**.

---

## 1️⃣ Create SSL Directory

RabbitMQ expects certificates to be stored securely.  
Create a dedicated SSL directory:

```bash
sudo mkdir -p /etc/rabbitmq/ssl
