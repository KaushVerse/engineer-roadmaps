# 🟩 NGINX Config Folders – **sites-available vs sites-enabled** (Deep Dive | Hinglish)

> 📄 **README.md**
> Is guide me NGINX ke **sites-available/** aur **sites-enabled/** folders ko **conceptually + practically** samjhaya gaya hai — real-world use cases, flow diagrams, commands, aur best practices ke saath.
> Agar ye clear ho gaya → NGINX production configs tumhare control me 🔥

---

## 🤔 Problem Statement (Bro wali confusion)

> **“sites-available aur sites-enabled dono kyu hote hain? conf.d me multiple domains ho to kya inki zarurat hoti hai?”**

👉 Short answer: **Depends on style** ❌/✅
👉 Long answer: **Neeche crystal clear** 😎

---

## 🧠 NGINX Config Loading Truth (MOST IMPORTANT)

NGINX sirf wahi config read karta hai jo `nginx.conf` me **include** hota hai:

```nginx
http {
    include /etc/nginx/mime.types;
    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
}
```

📌 **Rule:**

> Jis folder ko include kiya hai, **sirf wahi load hoga**.
> Folder ka naam important nahi, **include line important hai**.

---

# 1️⃣ sites-available/ – 💾 Configuration Library

### 📖 Concept

* Ye folder **store room / library** jaisa hai
* Yahan **saare possible site configs** rakhe jaate hain
* **By default inactive** hote hain

```text
/etc/nginx/sites-available/
 ├── example.com
 ├── api.example.com
 └── test.example.com
```

### 📄 Example Config

```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/example.com/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

📌 Sirf yahan file hone se site **LIVE nahi hoti**.

---

# 2️⃣ sites-enabled/ – ⚡ Active Sites Only

### 📖 Concept

* Ye folder **switch board** jaisa hai ⚡
* Sirf **active sites ke symlinks** hote hain
* NGINX **sirf isi folder ko read karta hai**

```text
/etc/nginx/sites-enabled/
 └── example.com -> ../sites-available/example.com
```

### 🔗 Site Activate Karna

```bash
sudo ln -s /etc/nginx/sites-available/example.com \
           /etc/nginx/sites-enabled/
```

### ❌ Site Deactivate Karna

```bash
sudo rm /etc/nginx/sites-enabled/example.com
```

📌 Original config **safe rehti hai** in `sites-available/` 💾

---

# 3️⃣ Flow Diagram (Mental Picture)

```text
/etc/nginx/sites-available/
 ├── example.com        (inactive config)
 ├── api.example.com

/etc/nginx/sites-enabled/
 ├── example.com  -> ../sites-available/example.com   (ACTIVE)
```

---

# 4️⃣ conf.d/ – ⚡ Auto-Active Style

### 📖 Concept

* `conf.d/` me jo bhi `*.conf` file hai
* **Sab automatically active** hote hain

```text
/etc/nginx/conf.d/
 ├── api.example.com.conf
 ├── admin.example.com.conf
 └── grafana.example.com.conf
```

📌 Jaise hi file banayi + reload → site live 🚀

---

# 5️⃣ conf.d vs sites-available Style (Truth Table)

| Scenario                | conf.d | sites-available | sites-enabled |
| ----------------------- | ------ | --------------- | ------------- |
| Docker 🐳               | ✅      | ❌               | ❌             |
| Kubernetes / ECS        | ✅      | ❌               | ❌             |
| Simple reverse proxy    | ✅      | ❌               | ❌             |
| Production VM           | ❌      | ✅               | ✅             |
| Multiple domains (prod) | ❌      | ✅               | ✅             |
| Mixed usage             | ⚠️     | ⚠️              | ⚠️            |

---

# 6️⃣ Dono ko ek saath use kar sakte hain kya? 🤯

```nginx
include /etc/nginx/conf.d/*.conf;
include /etc/nginx/sites-enabled/*;
```

✅ Technically allowed
❌ **Practically BAD idea**

### ☠️ Problems

* Same domain 2 baar load
* Port 80/443 conflict
* Debugging nightmare 💀

📌 **Rule:**

> 🧠 **Ek server = ek style**

---

# 7️⃣ Best Practices (Real World)

### 🧱 Production VM / Bare Metal

✅ Use:

```text
sites-available/
sites-enabled/
```

**Why?**

* Easy enable / disable
* Safer rollbacks
* Clean control

---

### 🐳 Docker / Cloud / Infra

✅ Use:

```text
conf.d/
```

**Why?**

* Simple
* Immutable infra
* No symlink drama

---

# 8️⃣ After Any Change – Mandatory Steps

```bash
sudo nginx -t              # config test
sudo systemctl reload nginx
```

❌ Reload ke bina change apply nahi hoga

---

# 🏁 Final Mental Model

> **sites-available = config bank** 💾
> **sites-enabled = active switches** ⚡
> **conf.d = auto-on system** 🚀

Samajh gaye to NGINX tumhara ho gaya 😎

---

## 🔥 Bro Tip

> **Production me control chahiye → sites-enabled**
> **Infra / containers me speed chahiye → conf.d**

📌 Happy Reverse Proxying 🚀🟩
