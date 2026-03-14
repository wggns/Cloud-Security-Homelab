# Install Docker on Ubuntu Server & Deploy Monitoring Stack

## Overview
This guide covers installing Docker, Docker Compose, and deploying a monitoring stack using **Prometheus** and **Grafana** on Ubuntu Server.

---

## 1. Update Ubuntu Server

First, update the system packages:
```bash
sudo apt update
sudo apt upgrade -y
```

---

## 2. Install Docker

Install Docker:
```bash
sudo apt install docker.io -y
```

Enable and start the Docker service:
```bash
sudo systemctl enable docker
sudo systemctl start docker
```

Verify the Docker version:
```bash
sudo docker --version
```

---

## 3. Install Docker Compose

Install Docker Compose:
```bash
sudo apt install docker-compose -y
```

Verify the version:
```bash
docker-compose --version
```

> At this point, Docker and Docker Compose are fully installed and ready to use.

---

## 4. Create Monitoring Stack Directory

Create a project folder:
```bash
mkdir monitoring-stack
cd monitoring-stack
```

Inside this directory, create the required configuration files:
```bash
nano docker-compose.yml
nano prometheus.yml
```

> Grafana configuration is handled inside the Docker Compose file.

---

## 5. Editing YAML Files (Why I Used SSH)

Editing YAML files directly in Ubuntu Server using nano can be difficult due to:
- Strict indentation requirements
- Spacing sensitivity in YAML
- Limited copy/paste functionality in CLI

To improve workflow, I used **SSH** from my Windows laptop to remotely manage the Ubuntu Server.

### Find Ubuntu Server IP Address

On Ubuntu Server, run:
```bash
hostname -I
```

This returns the internal LAN IP address (example: `192.168.1.50`)

> **Note:** The IP address may change if DHCP is enabled.

### Connect via SSH (From Windows)

On Windows PowerShell:
```powershell
ssh username@192.168.1.50
```

After entering the password, I was connected to the Ubuntu Server remotely.

**Benefits of SSH:**
- Clean copy/paste of YAML configurations
- Avoided indentation errors
- More efficient file management

---

## 6. Docker Compose Configuration

### docker-compose.yml
```yaml
version: '3'

services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - "3000:3000"
```

### prometheus.yml
```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
```

---

## 7. Launch the Monitoring Stack

Start the containers:
```bash
sudo docker-compose up -d
```

Verify containers are running:
```bash
sudo docker ps
```

If successful, you should see:
- ✅ Prometheus running on port `9090`
- ✅ Grafana running on port `3000`

---

## 8. Accessing Prometheus & Grafana

From your laptop web browser:

| Service | URL |
|---------|-----|
| Prometheus | http://192.168.1.50:9090 |
| Grafana | http://192.168.1.50:3000 |

---

## 9. Connecting Grafana to Prometheus

In Grafana:
1. Go to **Settings**
2. Select **Data Sources**
3. Click **Add data source**
4. Choose **Prometheus**
5. Enter URL: `http://prometheus:9090`
6. Click **Save & Test** to confirm the connection

> This works because both containers are running inside the same Docker network.

---

## 10. Architecture Overview

| Component | Role |
|-----------|------|
| Ubuntu Server | Runs Docker containers (Prometheus + Grafana) |
| Kali Linux | Simulates attacks |
| Laptop | Acts as management console |

All devices connect through:
- Managed switch
- Firewall
- Internal LAN

> Grafana was accessed from my laptop through the internal network only. Services were **not** exposed to the public internet, keeping the lab environment secure.

---

## 11. Purpose of This Setup

| Tool | Purpose |
|------|---------|
| Prometheus | Collects system metrics |
| Grafana | Visualizes collected data |
| Kali Linux | Simulates attack traffic |
| Ubuntu Server | Logs and monitors activity |

This setup allows me to:
- Simulate real-world attack scenarios
- Monitor system behavior under attack
- Validate detection visibility
- Practice defensive monitoring workflows

