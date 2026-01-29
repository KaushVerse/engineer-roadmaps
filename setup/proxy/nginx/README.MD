# ❇️ NGINX – Production Reverse Proxy & SSL Setup

This guide explains **production‑grade NGINX setup** for APIs, dashboards (Grafana, Jenkins), and RabbitMQ UI with **HTTP → HTTPS**, **Certbot**, and **multi‑domain routing**.

---

## 🧱 Architecture Overview

```
Internet 🌍
   │
   ▼
NGINX (80 / 443)
   │
   ├── api.twosouls.kaushverse.com   → 127.0.0.1:5000
   ├── grafana.kaushverse.com        → 127.0.0.1:3000
   ├── jenkins.kaushverse.com        → 127.0.0.1:8080
   └── rmq.kaushverse.com            → 127.0.0.1:15672
```

NGINX acts as:

* 🔁 Reverse Proxy
* 🔐 SSL Termination
* 🌐 Single public entrypoint

---

## ✅ STEP 1: Install NGINX (Host Machine)

```bash
sudo apt update
sudo apt install nginx -y
```

Check status:

```bash
sudo systemctl status nginx
```

---

## ✅ STEP 2: Single Domain Reverse Proxy (API Example)

Create config file:

```bash
sudo nano /etc/nginx/sites-available/api.conf
```

Paste:

```nginx
server {
    listen 80;
    server_name api.twosouls.kaushverse.com;

    location / {
        proxy_pass http://127.0.0.1:5000;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_cache_bypass $http_upgrade;
    }
}
```

Save & exit: `CTRL + X → Y → Enter`

---

## ✅ STEP 3: Enable Site

```bash
sudo ln -s /etc/nginx/sites-available/api.conf /etc/nginx/sites-enabled/
```

(Optional but recommended)

```bash
sudo rm /etc/nginx/sites-enabled/default
```

Test & reload:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

---

## ✅ STEP 4: DNS Verification

```bash
ping api.twosouls.kaushverse.com
```

Must resolve to your server IP.

---

## ✅ STEP 5: HTTP Test (MANDATORY)

Open in browser:

```
http://api.twosouls.kaushverse.com
```

⚠️ If HTTP does not work → **Certbot will fail**.

---

## 🔐 STEP 6: Enable HTTPS (Certbot)

Install certbot:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

Issue certificate:

```bash
sudo certbot --nginx -d api.twosouls.kaushverse.com
```

Choose:

```
2 → Redirect HTTP to HTTPS (recommended)
```

---

## 🔄 STEP 7: Auto‑Renewal Test

```bash
sudo certbot renew --dry-run
```

---

# 🌐 Multiple Domain Setup (PRODUCTION STYLE)

👉 **Do NOT use `sites-available / sites-enabled`**
👉 Use `conf.d/*.conf` (clean & scalable)

Directory:

```
/etc/nginx/
├── nginx.conf
└── conf.d/
    ├── grafana.conf
    ├── jenkins.conf
    └── rmq.conf
```

---

## 🧩 STEP 1: Ensure conf.d is Included

```bash
sudo nano /etc/nginx/nginx.conf
```

Inside `http {}` block:

```nginx
include /etc/nginx/conf.d/*.conf;
```

---

## 🧩 STEP 2: Grafana Config Example

```bash
sudo nano /etc/nginx/conf.d/grafana.conf
```

```nginx
server {
    listen 80;
    server_name grafana.kaushverse.com;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

---

## 🧩 STEP 3: Jenkins & RabbitMQ (Same Pattern)

### Jenkins

```nginx
server {
    listen 80;
    server_name jenkins.kaushverse.com;

    location / {
        proxy_pass http://127.0.0.1:8080;
    }
}
```

### RabbitMQ Management UI

```nginx
server {
    listen 80;
    server_name rmq.kaushverse.com;

    location / {
        proxy_pass http://127.0.0.1:15672;
    }
}
```

---

## 🔄 STEP 4: Reload NGINX

```bash
sudo nginx -t
sudo systemctl reload nginx
```

---

## 🌐 STEP 5: HTTP TEST (VERY IMPORTANT)

All must open on HTTP **before SSL**:

```
http://grafana.kaushverse.com
http://jenkins.kaushverse.com
http://rmq.kaushverse.com
```

---

## 🔐 STEP 6: SSL for Each Domain

```bash
sudo certbot --nginx -d grafana.kaushverse.com
sudo certbot --nginx -d jenkins.kaushverse.com
sudo certbot --nginx -d rmq.kaushverse.com
```

---

## 🛡️ Production Best Practices

* ✅ Always test **HTTP first**, then SSL
* ❌ Never expose backend ports publicly
* 🔐 Use HTTPS only for users
* 🔍 Monitor cert expiry
* 📦 One service = one `.conf`

---

## 🧠 Common Failures

| Issue            | Reason               |
| ---------------- | -------------------- |
| Certbot fails    | HTTP not reachable   |
| 502 Bad Gateway  | Backend service down |
| Wrong site opens | server_name mismatch |

---

## ✅ Final Checklist

* [ ] DNS points to server
* [ ] HTTP works
* [ ] SSL issued
* [ ] Auto‑renew OK
* [ ] Backends private

---

🔥 **This setup is production‑ready, scalable, and DevOps‑approved.**
