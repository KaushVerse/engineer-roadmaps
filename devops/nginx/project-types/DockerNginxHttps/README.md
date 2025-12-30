# 🌐 NGINX Reverse Proxy with HTTPS (Docker + Let’s Encrypt)

> 📄 **README.md**
> Ye guide ek **complete production-style architecture** explain karta hai jahan:
>
> **User (HTTPS)** → **NGINX (Docker Reverse Proxy)** → **SSL (Let’s Encrypt + Certbot)** → **Backend / Frontend Docker Apps**
>
> Sab kuch **step-by-step, Hinglish, real-world DevOps mindset** ke saath 🔥

---

## 🧠 High-Level Architecture (Mental Model)

```
User (Browser / Mobile App)
        ↓ HTTPS
NGINX (Docker Container)
        ↓ Internal Docker Network
Frontend / Backend Apps (Docker)
```

📌 **SSL termination NGINX pe hoti hai**
📌 Backend containers ko HTTPS ka load nahi pata hota

---

## 🏗 Components Breakdown (One-by-One)

### 1️⃣ 👤 User (Client)

* Browser / Mobile App
* Sirf **HTTPS (443)** se baat karta hai
* SSL certificate verify karta hai 🔒

---

### 2️⃣ 🌐 NGINX (Docker – Reverse Proxy)

**Role:**

* Internet-facing entry point
* SSL terminate karta hai
* Traffic route karta hai

**Why Reverse Proxy?**

* Multiple apps → single IP
* Central SSL handling
* Security + scalability

---

### 3️⃣ 🔒 SSL – Let’s Encrypt + Certbot

**Kaam:**

* Free trusted SSL certificates
* Auto-renew every 90 days

**Certificates yahan hote hain:**

```
/etc/letsencrypt/live/example.com/
├── fullchain.pem
├── privkey.pem
```

📌 NGINX inko mount karke use karta hai

---

### 4️⃣ ⚙️ Backend / Frontend Apps (Docker)

**Examples:**

* React frontend
* Node.js / Java / Python backend
* Grafana / Jenkins / RabbitMQ UI

📌 Ye apps **private Docker network** me rehte hain
📌 Internet se directly exposed ❌

---

## 🧠 Docker Networking Truth

```text
Internet
  ↓
[ NGINX Container ]  ← public ports (80, 443)
        ↓
[ App Containers ]  ← internal ports only
```

➡️ Security + isolation

---

## 📂 Recommended Folder Structure

```
project/
├── nginx/
│   ├── nginx.conf
│   ├── conf.d/
│   │   ├── frontend.conf
│   │   └── backend.conf
│   └── certbot/
├── certbot/
│   ├── conf/        # /etc/letsencrypt
│   └── www/         # ACME challenge
├── frontend/
├── backend/
└── docker-compose.yml
```

---

## 🐳 docker-compose.yml (Core File)

```yaml
version: "3.9"

services:
  nginx:
    image: nginx:latest
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/conf.d:/etc/nginx/conf.d
      - ./certbot/conf:/etc/letsencrypt
      - ./certbot/www:/var/www/certbot
    depends_on:
      - frontend
      - backend

  certbot:
    image: certbot/certbot
    volumes:
      - ./certbot/conf:/etc/letsencrypt
      - ./certbot/www:/var/www/certbot

  frontend:
    build: ./frontend
    expose:
      - "3000"

  backend:
    build: ./backend
    expose:
      - "8080"
```

---

## 🌐 NGINX Reverse Proxy Config (Example)

### frontend.conf

```nginx
server {
    listen 443 ssl;
    server_name frontend.example.com;

    ssl_certificate /etc/letsencrypt/live/frontend.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/frontend.example.com/privkey.pem;

    location / {
        proxy_pass http://frontend:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $remote_addr;
    }
}
```

---

## 🔑 SSL Certificate Generate (First Time)

```bash
docker compose run --rm certbot certonly \
  --webroot \
  --webroot-path=/var/www/certbot \
  -d frontend.example.com
```

---

## 🔄 Auto Renewal (Cron Style)

```bash
0 0 * * * docker compose run --rm certbot renew && docker compose restart nginx
```

---

## 🔐 Security Benefits

✅ Single exposed container
✅ No backend port leakage
✅ Central SSL
✅ Easy rate limiting / auth / WAF later

---

## ⚠️ Common Mistakes (Real World)

❌ Backend ko port expose karna
❌ SSL backend pe lagana
❌ Wrong Docker network
❌ Forgetting renew

---

## 🏁 Final Mental Model

> **NGINX = Gatekeeper** 🛡️
> **SSL = Identity proof** 🪪
> **Docker apps = private rooms** 🏠

Agar ye clear hai → tum production-ready ho 😎🔥

---

## 🔥 Bro Tip

> **Production me SSL aur routing central rakho – life easy rahegi** 💪

📌 Happy Shipping Secure Systems 🚀🔒
