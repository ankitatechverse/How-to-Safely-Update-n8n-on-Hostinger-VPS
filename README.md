# How to Safely Update n8n on Hostinger VPS

This guide walks you step-by-step through safely updating your n8n instance on a Hostinger VPS — without losing workflows, credentials, or execution history.

Hostinger’s n8n VPS comes with Docker + Docker Compose pre-installed and uses persistent volumes, which means your data stays safe even when containers are recreated.

---

## 📌 Table of Contents

* **0. Check if Docker is Installed**
* **1. Access Hostinger VPS Terminal**
* **2. (Optional) Clear Terminal**
* **3. Pull Latest n8n Image**
* **4. Stop Current n8n Container**
* **5. Start n8n Using Updated Image**
* **6. Confirm n8n is Running**
* **7. Confirm Updated n8n Version**
* **Data Persistence Explained**
* **Support**
* **License**
* **Author**

---

## 0. Check if Docker is Installed

Before updating n8n, make sure Docker is installed and working.

```
docker -v
```

If Docker is installed, you’ll see something like:

```
Docker version 28.5.1
```

If Docker is not installed, install it using:

```
curl -fsSL https://get.docker.com | sudo sh
```

---

## 1. Access Hostinger VPS Terminal

Go to:
**hPanel → VPS → Terminal**

Run all update commands here.

---

## 2. (Optional) Clear Terminal

Just for clean output:

```
clear
```

---

## 3. Pull Latest n8n Image

Make sure you're inside the folder containing your `docker-compose.yml`.

```
docker compose pull n8n
```

Verify directory:

```
ls
```

---

## 4. Stop Current n8n Container

This stops the old container without deleting your data.

```
docker compose down
```

---

## 5. Start n8n Using Updated Image

```
docker compose up -d
```

---

## 6. Confirm n8n is Running

```
docker compose ps
```

Look for **running** state.

---

## 7. Confirm Updated n8n Version

```
docker exec -it root-n8n-1 n8n -v
```

If unsure of container name:

```
docker ps
```

---

# 🔒 Data Persistence Explained

Hostinger’s setup uses a persistent volume:

```
volumes:
  - ~/.n8n:/home/node/.n8n
```

This keeps:

* Workflows
* Credentials
* Execution history
* All user data

safe during updates.

---
