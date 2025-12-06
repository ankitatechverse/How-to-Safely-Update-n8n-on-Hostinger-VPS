# How to Safely Update n8n on Hostinger VPS

This guide walks you step-by-step through safely updating your n8n instance on a Hostinger VPS — without losing workflows, credentials, or execution history.

Hostinger’s n8n VPS comes with Docker + Docker Compose pre-installed and uses persistent volumes, which means your data stays safe even when containers are recreated.

## Check Your Current n8n Version

* Open your self-hosted n8n dashboard.
* Look at the bottom of the page or in the Settings section to see the current n8n version.
* If your version is older than the latest release, an update is needed.
* Log in to Hostinger’s hPanel.
* Go to the **VPS menu** and click the **Terminal** button in the top-right corner.
* A black terminal window will open — this is where all update commands will be run.
* All commands in this guide are also available in the GitHub repo link or Medium article link.

## 1. Check if Docker is Installed

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
