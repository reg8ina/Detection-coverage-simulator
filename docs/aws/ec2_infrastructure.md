# EC2 Infrastructure Overview

This document describes the EC2 infrastructure built for the AWS Cloud Security Project.  
It includes a Bastion Host, Splunk Enterprise Server, and Web Server with Universal Forwarder.  
All components run inside a custom VPC and communicate using private IP addresses.

---

## EC2 Instances Summary

### 🔹 **Bastion Host — regi-bastion-ec2**
```
Public IP:       18.195.148.236
Private IP:      10.0.13.23
Instance Type:   t3.micro
Security Group:  regi-bastion-sg
Role:            Secure SSH entry point into the VPC
```

---

### 🔹 **Splunk Server — regi-splunk-server**
```
Public IP:       3.120.190.194
Private IP:      10.0.0.149
Instance Type:   t3.small
Security Group:  regi-splunk-sg
Role:            Splunk Enterprise (ports 8000, 9997)
```

---

### 🔹 **Web Server + Universal Forwarder — regi-web-ec2-new**
```
Public IP:       3.75.189.97
Private IP:      10.0.15.63
Instance Type:   t3.micro
Security Group:  regi-web-sg
Role:            Nginx Web Server + Splunk Universal Forwarder
```

---

### 📝 Legacy Instance
```
regi-web-ec2 — removed from architecture
```

---

## 🔧 Network Architecture

### VPC Details
```
VPC Name: regi-security-vpc-vpc
Region:   eu-central-1 (Frankfurt)
Subnets:  Public subnets
Routing:  Internet Gateway for outbound access
```

### Private Connectivity Flow
```
Bastion (10.0.13.23)
    → SSH
         → Web Server (10.0.15.63)
             → UF logs
                   → Splunk Server (10.0.0.149)
```

### Public Access Flow
```
Internet → Bastion Host (SSH only)
Internet → Web Server (HTTP via Nginx)
```

---

## Final Notes
The environment now contains **only three production EC2 instances**.  
The old web server instance was terminated to keep the architecture clean.

