Install Docker on Ubuntu Server & Deploy Monitoring Stack
1. Update Ubuntu Server

First, update the system packages:

sudo apt update
sudo apt upgrade -y
2. Install Docker

Install Docker:

sudo apt install docker.io -y

Enable and start the Docker service:

sudo systemctl enable docker
sudo systemctl start docker

Verify the Docker version:

sudo docker --version
3. Install Docker Compose

Install Docker Compose:

sudo apt install docker-compose -y

Verify the version:

docker-compose --version

At this point, Docker and Docker Compose are fully installed and ready to use.

Create Monitoring Stack Directory

Create a project folder:

mkdir monitoring-stack
cd monitoring-stack

Inside this directory, create the required configuration files:

nano docker-compose.yml
nano prometheus.yml

Grafana configuration is handled inside the Docker Compose file.

Editing YAML Files (Why I Used SSH)

Editing YAML files directly in Ubuntu Server using nano can be difficult due to:

Strict indentation requirements

Spacing sensitivity in YAML

Limited copy/paste functionality in CLI

To improve workflow, I used SSH from my Windows laptop to remotely manage the Ubuntu Server.

Find Ubuntu Server IP Address

On Ubuntu Server, run:

hostname -I

This returns the internal LAN IP address (example: 192.168.1.50).

Note: The IP address may change if DHCP is enabled.

Connect via SSH (From Windows)

On Windows PowerShell:

ssh username@192.168.1.50

After entering the password, I was connected to the Ubuntu Server remotely.

Benefits of SSH:

Clean copy/paste of YAML configurations

Avoided indentation errors

More efficient file management

Docker Compose Configuration
docker-compose.yml
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
prometheus.yml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
Launch the Monitoring Stack

Start the containers:

sudo docker-compose up -d

Verify containers are running:

sudo docker ps

If successful, you should see:

Prometheus running on port 9090

Grafana running on port 3000

Accessing Prometheus & Grafana

From your laptop web browser:

http://192.168.1.50:9090
http://192.168.1.50:3000

Port 9090 → Prometheus

Port 3000 → Grafana

Connecting Grafana to Prometheus

In Grafana:

Go to Settings

Select Data Sources

Click Add data source

Choose Prometheus

Enter URL:

http://prometheus:9090

This works because both containers are running inside the same Docker network.

Click Save & Test to confirm the connection.

Architecture Overview

Ubuntu Server runs Docker containers (Prometheus + Grafana)

Kali Linux is used to simulate attacks

My laptop acts as the management console

All devices connect through:

Managed switch

Firewall

Internal LAN

Grafana was accessed from my laptop through the internal network only. The services were not exposed to the public internet, which keeps the lab environment secure.

Purpose of This Setup

Prometheus collects system metrics.

Grafana visualizes collected data.

Kali Linux simulates attack traffic.

Ubuntu logs and monitors activity.

This setup allows me to:

Simulate real-world attack scenarios

Monitor system behavior under attack

Validate detection visibility

Practice defensive monitoring workflows
