# Security-Homelab
 Security monitoring lab from scratch using Kali Linux, Ubuntu Server, Docker, Prometheus, Grafana and Fail2ban to simulate and detect SSH brute-force attacks.

# Security Homelab

## Project Overview
Designed and deployed a Linux-based cloud security monitoring lab from scratch. 
Simulated SSH brute-force attacks using Kali Linux and implemented automated detection and blocking using Fail2ban. 
Monitoring stack deployed using Docker with Prometheus and Grafana for observability.

---

## Architecture

- Attacker Machine: Kali Linux
- Target / Logging Server: Ubuntu Server
- Containerization: Docker
- Monitoring: Prometheus + Grafana
- Detection & Response: Fail2ban
- Network Segmentation: Managed switch + firewall

---

## Infrastructure Setup

### 1. Kali Linux Installation
- Installed Kali Linux as attacker machine
- Verified SSH connectivity to target
- Used Hydra to simulate brute-force attacks

### 2. Ubuntu Server Setup
- Installed Ubuntu Server
- Enabled SSH service
- Configured system logging

### 3. Docker Installation
- Installed Docker and Docker Compose
- Deployed Prometheus and Grafana containers

---

## Monitoring Stack

- Prometheus configured to scrape system metrics
- Grafana dashboard created for:
  - CPU usage
  - Memory usage
  - Network activity
  - SSH authentication attempts

---

## Detection Layer (Fail2ban)

- Configured Fail2ban to monitor `/var/log/auth.log`
- Automatically bans IPs after multiple failed SSH attempts
- Verified bans using:


Observed:
- Multiple failed login attempts
- Fail2ban triggered
- Attacker IP banned automatically

---

## Key Skills Demonstrated

- Linux Administration
- Docker Containerization
- Log Monitoring
- Intrusion Detection
- Incident Response Automation
- Cloud Security Concepts

---

## Future Improvements

- Deploy monitoring stack on AWS EC2
- Integrate CloudWatch logging
- Automate infrastructure using Terraform
  
