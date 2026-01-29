# 🔐 Grafana – Admin Security & Access Setup (Production)

This document explains **secure, production-grade ways** to manage **Grafana admin credentials** across **VM, Docker, and Kubernetes** setups.

---

## 🧱 Security Philosophy (Read First)

* 🔐 **Admin credentials must be deterministic** (no surprises on reboot)
* 📦 **Config > CLI > Env** (priority depends on deployment)
* ❌ Never hardcode secrets in Git
* ✅ Rotate passwords regularly

---

## ✅ OPTION 1: Grafana Config File (Permanent & Clean)

👉 Best for **VM / EC2 / Bare-metal** setups

---

### 1️⃣ Open Grafana Config

```bash
sudo nano /etc/grafana/grafana.ini
```

---

### 2️⃣ Update `[security]` Section

Search for:

```ini
[security]
```

Add / update:

```ini
[security]
admin_user = grafana_admin
admin_password = StrongGrafana@123
```

📌 Notes:

* Applies **only on first startup**
* If admin already exists → password will NOT change

---

### 3️⃣ Restart Grafana

```bash
sudo systemctl restart grafana-server
```

Verify:

```bash
sudo systemctl status grafana-server
```

---

### 4️⃣ Login

```
http://<SERVER_IP>:3000
```

Credentials:

```
Username: grafana_admin
Password: StrongGrafana@123
```

---

## ✅ OPTION 2: Grafana CLI (MOST USED 🔥)

👉 Best for **existing installations**
👉 Safest way to **rotate admin password**

---

### Reset Admin Password

```bash
sudo grafana-cli admin reset-admin-password StrongGrafana@123
```

Login:

```
Username: admin
Password: StrongGrafana@123
```

📌 Notes:

* Works even if UI login is broken
* Does NOT require Grafana restart

---

## ✅ OPTION 3: Environment Variables (Docker / K8s)

👉 Best for **containers & GitOps**

---

### Supported Variables

```bash
GF_SECURITY_ADMIN_USER=grafana_admin
GF_SECURITY_ADMIN_PASSWORD=StrongGrafana@123
```

---

### 🐳 Docker Example

```yaml
environment:
  - GF_SECURITY_ADMIN_USER=grafana_admin
  - GF_SECURITY_ADMIN_PASSWORD=StrongGrafana@123
```

---

### ☸️ Kubernetes Example

```yaml
env:
  - name: GF_SECURITY_ADMIN_USER
    valueFrom:
      secretKeyRef:
        name: grafana-secret
        key: admin-user

  - name: GF_SECURITY_ADMIN_PASSWORD
    valueFrom:
      secretKeyRef:
        name: grafana-secret
        key: admin-password
```

---

## 🛡️ Production Best Practices

* 🔐 Always use **strong passwords**
* ❌ Never expose Grafana directly on port 3000
* 🌐 Put Grafana behind **NGINX + HTTPS**
* 👥 Create **Viewer / Editor users**, avoid admin usage
* 🔄 Rotate credentials periodically

---

## 🔥 Recommended Setup (Real Production)

```
Internet
   │
   ▼
NGINX (HTTPS)
   │
   ▼
Grafana (localhost:3000)
```

* Port 3000 → localhost only
* Access via [https://grafana.yourdomain.com](https://grafana.yourdomain.com)

---

## 🧠 Common Issues

| Issue                 | Reason                 | Fix                |
| --------------------- | ---------------------- | ------------------ |
| Password not changing | Admin already exists   | Use CLI            |
| Login fails           | Cached browser session | Logout / Incognito |
| Grafana exposed       | Direct port open       | Firewall / NGINX   |

---

## ✅ Final Checklist

* [ ] Admin password rotated
* [ ] Port 3000 not public
* [ ] HTTPS enabled
* [ ] Secrets not in Git
* [ ] Non-admin users created

---

🔥 **This setup is secure, clean, and production-approved.**
