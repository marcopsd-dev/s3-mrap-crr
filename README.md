# 🌍 Secure Multi-Region S3 Architecture  
### Cross-Region Replication (CRR) & Multi-Region Access Points (MRAP)

![AWS](https://img.shields.io/badge/AWS-S3-orange)
![Security](https://img.shields.io/badge/Security-High-green)
![Availability](https://img.shields.io/badge/Availability-Multi--Region-blue)
![Encryption](https://img.shields.io/badge/Encryption-KMS-yellow)
![Compliance](https://img.shields.io/badge/Compliance-Ready-success)

---

## 📑 Table of Contents

- [Description](#-description)
- [Architecture at a Glance](#-architecture-at-a-glance)
- [Security & Resilience Highlights](#-security--resilience-highlights)
- [Event-Driven Security & Alerting](#-event-driven-security--alerting)
- [CloudFormation Stacks](#-cloudformation-stacks)

---

## 🧭 Description

This project implements a **secure, resilient, and compliance-ready Amazon S3 architecture** using **multi-region design principles** and **event-driven security monitoring**.

The solution combines **KMS-encrypted S3 buckets**, **Object Lock (WORM)**, and **Object Versioning** to protect data against accidental deletion, ransomware, and insider threats. **Cross-Region Replication (CRR)** ensures data durability and disaster recovery, while **Multi-Region Access Points (MRAP)** provide low-latency global access.

Security visibility and automation are enhanced using:
- **Amazon Macie** for sensitive data discovery
- **Amazon EventBridge** for security event routing
- **Amazon SNS** for real-time alerts
- **AWS CloudTrail & CloudWatch** for centralized logging and auditing

This architecture is well-suited for **regulated environments**, **forensics readiness**, and **zero-trust cloud security models**.

---

## 🏗️ Architecture at a Glance

| Tool | Description |
|------|------------|
| 🪣 **S3 Buckets (Multi-Region)** | Regionally isolated buckets for resilience, availability, and fault tolerance |
| 🌐 **Cross-Region Replication (CRR)** | Automatically replicates objects and versions across regions |
| 🚀 **Multi-Region Access Points (MRAP)** | Global endpoint that routes traffic to the nearest healthy bucket |
| 🔐 **AWS KMS (CMKs)** | Customer-managed encryption keys per region |
| 🧱 **S3 Object Lock (WORM)** | Immutable storage preventing deletion or modification |
| 🔄 **S3 Object Versioning** | Maintains historical versions for rollback and recovery |
| 🧾 **AWS CloudTrail** | Captures S3, KMS, IAM, and API activity for auditing |
| 📊 **Amazon CloudWatch** | Metrics, logs, and alarms for operational and security monitoring |
| 🕵️ **Amazon Macie** | Detects and classifies sensitive data in S3 |
| ⚡ **Amazon EventBridge** | Routes Macie findings and API events |
| 📣 **Amazon SNS** | Sends security alerts and notifications |
| 🧾 **IAM Policies & Roles** | Enforces least-privilege access across services |

---

## 🔐 Security & Resilience Highlights

| Control | MITRE ATT&CK Technique | ID | Security Benefit |
|-------|------------------------|----|------------------|
| 🪣 **Multi-Region S3** | Data from Cloud Storage | T1530 | Prevents data loss via geographic redundancy |
| 🌐 **CRR** | Data Encrypted for Impact | T1486 | Preserves clean copies during ransomware events |
| 🚀 **MRAP** | Network Service Discovery | T1046 | Maintains service availability during regional failures |
| 🔐 **KMS CMKs** | Unsecured Credentials | T1552 | Protects data confidentiality at rest |
| 🧱 **Object Lock (WORM)** | Inhibit System Recovery | T1490 | Prevents deletion or tampering of backups |
| 🔄 **Object Versioning** | Data Destruction | T1485 | Enables rollback after accidental or malicious changes |
| 🧾 **CloudTrail Logging** | Modify Cloud Compute Infrastructure | T1578 | Detects unauthorized configuration changes |
| 📊 **CloudWatch Alerts** | Account Manipulation | T1098 | Flags abnormal access or policy changes |
| 🕵️ **Amazon Macie** | Data from Cloud Storage | T1530 | Identifies sensitive data exposure |
| ⚡ **EventBridge + SNS** | Command and Control | T1105 | Enables near-real-time incident response |

---

## ⚡ Event-Driven Security & Alerting

This architecture leverages **event-driven automation** to detect and respond to security risks in near real time.

**Flow Overview:**

1. **Amazon Macie** scans S3 buckets for sensitive data
2. **Macie findings** are published to **Amazon EventBridge**
3. **EventBridge rules** filter high-severity findings
4. **Amazon SNS** sends alerts to security teams
5. **CloudTrail & CloudWatch** provide investigation context

**Benefits:**
- Faster detection of data exposure
- Reduced mean time to respond (MTTR)
- Centralized, auditable alerting
- SOC-ready security telemetry

---

## ☁️ CloudFormation Stacks

### 📦 [JSON Stack #1 – Secure S3 Core](S3_Bucket_CFN_JSON)

**Description:**  
Creates a hardened S3 bucket with **Object Lock**, **Versioning**, **KMS encryption**, and **restricted IAM access**, along with a **dedicated immutable logging bucket**.

**Stack Diagram:**  
<img width="7659" height="2742" alt="S3_UPDATED_STACK_1" src="https://github.com/user-attachments/assets/8e99ceb6-272b-4335-8b6e-ccde6265a499" />

---

### 📦 [JSON Stack #2 – Replication Bucket](s3_bucket_region_2)

**Description:**  
Deploys additional region-specific S3 buckets configured for **CRR**, **Object Lock**, **Versioning**, and **KMS encryption**.

**Stack Diagram:**  
<img width="6484" height="544" alt="s3_Replicate_Bucket" src="https://github.com/user-attachments/assets/3c3cbc19-6458-4f31-91bf-12af5f1bedba" />

---

### 📦 [JSON Stack #3 – CRR & MRAP](S3_CRR_MRAP)

**Description:**  
Enables **Cross-Region Replication** and configures a **Multi-Region Access Point** for unified global access while maintaining encryption and compliance controls.

**Stack Diagram:**  
<img width="6228" height="591" alt="s3_CRR_MRAP" src="https://github.com/user-attachments/assets/7a45a333-933d-4f08-818f-2e662164d3f0" />

---

## ✅ Use Cases

- Ransomware-resistant backups
- Compliance-driven storage (SEC 17a-4, HIPAA, GDPR)
- Global application data access
- Forensics & audit readiness
- Zero-trust cloud architectures

---

## 🛡️ Security Mindset

> **Assume breach. Design for recovery. Detect everything.**

This project emphasizes **prevention, detection, and recovery**—not just availability.

---

