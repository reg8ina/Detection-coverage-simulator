# EC2 Infrastructure Overview  
AWS Cloud Security Project

---

## Overview

This document describes the EC2-based infrastructure used in the AWS Cloud Security Project.  
The environment includes a Bastion host, a Splunk Enterprise server, and a Web Server running Nginx with Universal 
Forwarder.  
All components are deployed inside a custom VPC and communicate using private IP addresses.

---

## EC2 Instances Summary

| Instance Name        | Public IP      | Private IP   | Instance Type | Security Group   | Role / Purpose                                   
|
|----------------------|----------------|--------------|----------------|------------------|---------------------------------------------------|
| regi-bastion-ec2     | 18.195.148.236 | 10.0.13.23   | t3.micro       | regi-bastion-sg  | Secure SSH entry point into the 
VPC              |
| regi-splunk-server   | 3.120.190.194  | 10.0.0.149   | t3.small       | regi-splunk-sg   | Splunk Enterprise (ports 8000, 
9997)             |
| regi-web-ec2-new     | 3.75.189.97    | 10.0.15.63   | t3.micro       | regi-web-sg      | Web server (Nginx + Universal 
Forwarder)         |

> *Legacy instance (regi-web-ec2) was removed from architecture.*

---

## Network Architecture

### Internal Flow (Private)

```
[Bastion 10.0.13.23]
        |
        | SSH
        v
[Web Server 10.0.15.63] ---- Logs (9997) ----> [Splunk 10.0.0.149]
```

### External Flow (Public)

- Your computer → SSH → Bastion  
- Your computer → HTTP (80) → Web Server  
- Your computer → Splunk Web UI (8000)

---

## Security Groups

### regi-bastion-sg
- Inbound: SSH (22) only from your IP  
- Outbound: Allow all  
- Purpose: Secure SSH access  

### regi-splunk-sg
- Inbound:
  - SSH (22) from Bastion  
  - Splunk Web (8000)  
  - Splunk ingestion (9997)
- Outbound: Allow all  
- Purpose: Splunk server  

### regi-web-sg
- Inbound:
  - SSH (22) from Bastion  
  - HTTP (80)
- Outbound:
  - Logs → Splunk (9997)
- Purpose: Nginx web server  

---

## Instance Roles

### Bastion Host
Secure access point to the private VPC network.

### Splunk Server
Runs Splunk Enterprise (8000) and receives logs on port 9997.

### Web Server
Nginx + Universal Forwarder sending logs to Splunk.

---

## Useful Commands

```
sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y
ss -tulnp
curl http://3.75.189.97
ping 10.0.0.149
sudo systemctl restart nginx
```

---

## Final Architecture Status

✔ Network works end-to-end  
✔ Bastion restricts SSH access  
✔ Web → Splunk logs flow confirmed  
✔ Infrastructure ready for SOC investigation  

