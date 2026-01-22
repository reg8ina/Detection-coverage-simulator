# 📘 Splunk + Docker Setup

## Overview
This document describes the complete setup of Splunk Enterprise using Docker.  
The goal is to create a reproducible, container-based Splunk environment for log ingestion, analysis, and security monitoring as part of the AWS Cloud Security Lab.

---

## 1️⃣ Prerequisites

Ensure the following tools are installed and working:

- **Docker Engine**  
- **Docker Compose (optional)**  
- **Git**  
- **Mac Terminal / Linux shell**

Verify Docker is running:

```bash
docker --version
docker ps
```

---

## 2️⃣ Create Persistent Docker Volumes for Splunk

Splunk requires persistent volumes so that logs and configuration are not lost between container restarts.

Create the volumes:

```bash
docker volume create splunk-etc
docker volume create splunk-var
```

Verify:

```bash
docker volume ls
```

---

## 3️⃣ Run Splunk Enterprise in Docker

Run the official Splunk Enterprise container from Docker Hub:

```bash
docker run -d \
  --name splunk \
  -p 8000:8000 \
  -p 8089:8089 \
  -p 9997:9997 \
  -e SPLUNK_START_ARGS="--accept-license" \
  -e SPLUNK_PASSWORD="MyStrongPassword123!" \
  -v splunk-etc:/opt/splunk/etc \
  -v splunk-var:/opt/splunk/var \
  splunk/splunk:latest
```

---

## 4️⃣ Verify Splunk is Running

Check the container status:

```bash
docker ps
```

View logs:

```bash
docker logs splunk
```

You should see Splunk initializing and then running normally.

---

## 5️⃣ Access Splunk Web Interface

Open your browser and navigate to:

👉 http://localhost:8000

Log in with:
- **Username:** `admin`  
- **Password:** The password you set earlier (e.g., `MyStrongPassword123!`)

---

## 6️⃣ Restart / Stop / Remove Splunk Container

Stop Splunk:

```bash
docker stop splunk
```

Start Splunk:

```bash
docker start splunk
```

Remove Splunk container:

```bash
docker rm -f splunk
```

---

## 7️⃣ Optional: Clean All Data (Reset Environment)

If you want a fresh Splunk instance:

```bash
docker volume rm splunk-etc
docker volume rm splunk-var
```

---

## ✔️ Status

Splunk Enterprise is now fully installed and running inside Docker.  
This environment is ready for connecting AWS log sources such as CloudTrail, GuardDuty, and VPC Flow Logs for security monitoring and analysis.

