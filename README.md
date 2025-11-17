# AWS Cloud Security Project

🌐 Project Overview
This project simulates a real-world cloud security monitoring and incident response environment.  
The goal is to design and implement an end-to-end security pipeline that includes logging, alerting, threat detection, and investigation processes using AWS native services and Splunk.

This repository documents the full lifecycle of the project — from environment setup, through data collection and analysis, to building SOC/IR methodologies.

---

## ✔️ Completed Work

### **1. Repository and Version Control Setup**
- Initialized a local Git repository and structured the project folders.
- Created a dedicated GitHub repository (`aws-cloud-security-project`).
- Configured remote origin and pushed the initial project commit.
- Added project documentation foundation (README).

---

## 🎯 Current Focus (Week 1 Objectives)
The following tasks were defined as part of the structured mentoring plan:

### **Environment Preparation**
- Set up AWS Free Tier environment for security testing and log collection.
- Review AWS core security concepts (IAM, S3, EC2 networking, logging architecture).
- Prepare IAM permissions according to least-privilege principles for lab use.

### **Security Logging Setup**
- Configure CloudTrail for audit logging (multi-region, management + data events).
- Prepare S3 bucket architecture for log storage.
- Enable GuardDuty for threat detection.

### **SIEM Integration**
- Prepare ingestion pipeline from AWS → Splunk.
- Plan data normalization and field extractions.
- Define detection use cases in SPL.

---

## 📌 Upcoming Milestones
The next development phases include:

### **Detection Engineering**
- Build SPL queries for identifying suspicious AWS API activity.
- Correlate CloudTrail events with GuardDuty findings.
- Develop dashboards for SOC monitoring purposes.

### **Incident Response Development**
- Create an IR workflow based on NIST standards.
- Document realistic attack scenarios and investigations.
- Build IR reports with:
  - Findings  
  - Impact  
  - Response  
  - Lessons Learned  

---

## 🛠 Technologies & Services
- **AWS:** CloudTrail, GuardDuty, IAM, S3, EC2  
- **Logging & SIEM:** Splunk Enterprise (Docker-based deployment)  
- **Security Frameworks:** NIST 800-61, AWS Well-Architected – Security Pillar  
- **Languages & Tools:** SPL, Bash, Git, Docker  

---

## 🎯 Project Purpose
This project is designed to demonstrate:
- Practical cloud security engineering skills  
- Ability to build real logging and detection infrastructure  
- Strong SOC/Tier 2–level investigation experience  
- Capability to design and manage end-to-end cloud security solutions  

---

## 👩‍💻 Author
Regina  
Cloud Security Engineer (In Progress) | SOC Analyst | Security Research Learner

---



