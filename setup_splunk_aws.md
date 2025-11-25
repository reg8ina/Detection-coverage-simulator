# Splunk Enterprise + Universal Forwarder on AWS  
Cloud Security Monitoring Deployment Guide

## Overview
This document provides a clean, professional setup guide for deploying **Splunk Enterprise** and the **Splunk Universal 
Forwarder (UF)** on AWS EC2 instances.  
The purpose of this deployment is to build a cloud-based security monitoring pipeline for centralized log collection, live 
visibility, and threat detection.

---

## Architecture Summary

**Components:**
- **Splunk Enterprise Server**
  - Ubuntu EC2 instance
  - Receives logs over TCP 9997
  - Hosts Splunk Web UI (port 8000)

- **Universal Forwarder Server**
  - Amazon Linux / Ubuntu EC2 instance
  - Sends system logs, Nginx logs, and security events to Splunk

- **AWS Infrastructure**
  - Custom VPC with public subnets
  - Security Groups configured for Splunk and SSH access

---

## 1. Splunk Enterprise Installation (Receiver)

### Install Splunk Enterprise
```bash
cd /tmp
sudo dpkg -i splunk-10.0.1-linux-amd64.deb
sudo /opt/splunk/bin/splunk start --accept-license
# Splunk Enterprise + Universal Forwarder on AWS
Cloud Security Monitoring Deployment Guide

## Overview
This document provides a clean, professional setup guide for deploying Splunk Enterprise and the Splunk Universal Forwarder 
(UF) on AWS EC2 instances. The purpose of this deployment is to build a cloud-based security monitoring pipeline for 
centralized log collection, live visibility, and threat detection.

## Architecture Summary
Components:
- Splunk Enterprise Server
  - Ubuntu EC2 instance
  - Receives logs over TCP 9997
  - Hosts Splunk Web UI (port 8000)

- Universal Forwarder Server
  - Amazon Linux / Ubuntu EC2 instance
  - Sends system logs, Nginx logs, and security events to Splunk

- AWS Infrastructure
  - Custom VPC with public subnets
  - Security Groups configured for Splunk and SSH access

## 1. Splunk Enterprise Installation (Receiver)

Install Splunk Enterprise:
cd /tmp
sudo dpkg -i splunk-10.0.1-linux-amd64.deb

Start Splunk and accept license:
sudo /opt/splunk/bin/splunk start --accept-license

Enable Splunk at boot:
sudo /opt/splunk/bin/splunk enable boot-start

Enable receiving logs (TCP 9997):
sudo /opt/splunk/bin/splunk enable listen 9997

Verify listener:
sudo ss -tulnp | grep 9997

Splunk Web UI:
http://<SPLUNK_PUBLIC_IP>:8000

## 2. Universal Forwarder Installation (Sender)

Amazon Linux (RPM):
sudo rpm -i splunkforwarder-10.x.x-linux-2.6-x86_64.rpm

Ubuntu/Debian:
sudo dpkg -i splunkforwarder-10.x.x-linux-amd64.deb

Start UF and accept license:
sudo /opt/splunkforwarder/bin/splunk start --accept-license

Enable boot-start:
sudo /opt/splunkforwarder/bin/splunk enable boot-start

## 3. Connect UF to Splunk Enterprise

Add forward-server (use private IP):
sudo /opt/splunkforwarder/bin/splunk add forward-server 10.0.0.149:9997 -auth admin:<password>

Verify connection:
sudo /opt/splunkforwarder/bin/splunk list forward-server

Expected output:
Active forwards:
    10.0.0.149:9997

## 4. Add Log Sources for Monitoring

System logs:
sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/messages
sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/secure

Nginx logs:
sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/nginx/

Restart UF:
sudo systemctl restart splunkforwarder

## 5. AWS Security Group Configuration

Splunk Enterprise SG (Inbound):
TCP 22 → Your IP
TCP 8000 → Any or management IPs
TCP 9997 → UF Instance Private IP

Universal Forwarder SG (Outbound):
TCP 9997 → Splunk Enterprise Private IP

## 6. Log Ingestion Verification (Splunk Search)

Verify incoming logs:
index=* host=<UF-HOSTNAME>

Check Nginx activity:
source="/var/log/nginx/access.log"

Check SSH authentication logs:
source="/var/log/auth.log"

Host metadata:
| metadata type=hosts

## 7. Attack Traffic for Testing

Nginx access simulation:
curl http://<WEB_SERVER_PUBLIC_IP>
curl -I http://<WEB_SERVER_PUBLIC_IP>

Failed SSH attempts:
ssh wrong@<SERVER_IP>

## 8. Troubleshooting

Check Splunk receiver:
ss -tulnp | grep 9997

Check UF forwarding status:
sudo /opt/splunkforwarder/bin/splunk list forward-server

Check monitored files:
sudo /opt/splunkforwarder/bin/splunk list monitor

Check SG rules alignment:
- UF → Splunk TCP 9997 allowed
- Splunk Web UI TCP 8000 reachable

## Final Status
Splunk Enterprise deployed on AWS
Universal Forwarder configured and forwarding logs
System, Nginx, and authentication logs ingested
Security pipeline functioning
Environment ready for attack simulation and SIEM analysis

