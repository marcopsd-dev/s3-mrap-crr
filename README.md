# 🌍 Secure Multi-Region S3 Architecture  
### Cross-Region Replication (CRR) & Multi-Region Access Points (MRAP)

![AWS](https://img.shields.io/badge/AWS-S3-orange)
![Security](https://img.shields.io/badge/Security-High-green)
![Availability](https://img.shields.io/badge/Availability-Multi--Region-blue)
![Encryption](https://img.shields.io/badge/Encryption-KMS-yellow)
![Compliance](https://img.shields.io/badge/Compliance-Ready-success)

---

## 📑 Table of Contents


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
<br>

| Component | Purpose | Key Features |
|-----------|---------|--------------|
| 👥 **Applications & Users** | Global client access layer | Multi-region routing, automatic failover |
| 🌐 **Multi-Region Access Point** | Intelligent request routing | Latency-based routing, health checks |
| 🪣 **S3 Buckets** | Dual-region storage | Active-passive configuration, CRR enabled |
| 🔄 **Versioning** | Data protection | Point-in-time recovery, accidental deletion protection |
| 🧱 **Object Lock** | Compliance & immutability | WORM storage, ransomware protection |
| 🔐 **KMS Encryption** | Data confidentiality | AES-256 encryption, automated key rotation |
| 🧾 **CloudTrail** | Audit logging | Complete API activity tracking, compliance evidence |
| 📦 **Central Logging** | Log aggregation | Cross-account logging, long-term retention |
| 🕵️ **Amazon Macie** | Data classification | Automated PII detection, sensitive data alerts |
| ⚡ **EventBridge** | Event orchestration | Real-time event filtering, automated workflows |
| 📊 **CloudWatch** | Operational monitoring | Custom metrics, anomaly detection, dashboards |
| 📣 **SNS Notifications** | Alert distribution | Multi-channel delivery, priority routing |
| 👨‍💼 **Security Operations** | Incident response | 24/7 monitoring, threat analysis, remediation |

<br>

### Architectural Diagram: 

<br>

```mermaid
flowchart TB
    %% Styling with vibrant colors on black background
    classDef clientClass fill:#4A90E2,stroke:#6DB3F2,stroke-width:3px,color:#000,font-weight:bold
    classDef mrapClass fill:#9B59B6,stroke:#BB8FCE,stroke-width:3px,color:#fff,font-weight:bold
    classDef s3Class fill:#FF6B35,stroke:#FF8C61,stroke-width:3px,color:#fff,font-weight:bold
    classDef securityClass fill:#2ECC71,stroke:#58D68D,stroke-width:3px,color:#000,font-weight:bold
    classDef loggingClass fill:#3498DB,stroke:#5DADE2,stroke-width:3px,color:#fff,font-weight:bold
    classDef monitorClass fill:#E74C3C,stroke:#EC7063,stroke-width:3px,color:#fff,font-weight:bold
    classDef alertClass fill:#F39C12,stroke:#F8C471,stroke-width:3px,color:#000,font-weight:bold
    classDef kmsClass fill:#16A085,stroke:#48C9B0,stroke-width:3px,color:#fff,font-weight:bold
    
    %% Application Layer
    A[👥 Applications & Users<br/>Global Access]:::clientClass
    
    %% Global Routing
    B[🌐 S3 Multi-Region Access Point<br/>& Automatic Failover]:::mrapClass
    
    %% Primary Storage
    C1[🪣 Primary Bucket<br/>Region: us-east-1<br/>Status: Active]:::s3Class
    
    %% Replica Storage
    C2[🪣 Replica Bucket<br/>Region: us-west-2<br/>Status: Standby]:::s3Class
    
    %% Data Protection Layer
    D[🔄 Versioning Enabled<br/>Complete History<br/>Rollback Ready]:::securityClass
    E[🧱 Object Lock<br/>WORM Compliance<br/>Immutable Storage]:::securityClass
    F1[🔐 KMS Key us-east-1<br/>Customer Managed<br/>Automatic Rotation]:::kmsClass
    F2[🔐 KMS Key us-west-2<br/>Customer Managed<br/>Automatic Rotation]:::kmsClass
    
    %% Audit Trail
    G[🧾 AWS CloudTrail<br/>API Call Logging<br/>Cross-Region Enabled]:::loggingClass
    H[📦 Logging Bucket<br/>Central Repository<br/>Long-Term Retention]:::loggingClass
    I[🔒 Tamper-Proof Logs<br/>Object Lock Active<br/>Forensics Ready]:::loggingClass
    
    %% Threat Detection
    J[🕵️ Amazon Macie<br/>Sensitive Data Discovery<br/>PII Detection]:::monitorClass
    K[⚡ EventBridge Rules<br/>Real-Time Filtering<br/>Automated Routing]:::monitorClass
    N[📊 CloudWatch<br/>Metrics & Dashboards<br/>Anomaly Detection]:::monitorClass
    
    %% Alert System
    L[📣 SNS Notifications<br/>Multi-Channel Alerts<br/>Email & Slack]:::alertClass
    M[👨‍💼 Security Operations<br/>24/7 Monitoring<br/>Incident Response]:::alertClass
    
    %% Primary Flow
    A -->|HTTPS Requests| B
    B -->|Route to Primary| C1
    B -->|Route to Replica| C2
    C1 -.->|Async Replication<br/>Real-Time Sync| C2
    
    %% Security Controls
    C1 -->|Applied to| D
    C2 -->|Applied to| D
    C1 -->|Protected by| E
    C2 -->|Protected by| E
    C1 -->|Encrypted with| F1
    C2 -->|Encrypted with| F2
    
    %% Audit Pipeline
    C1 -->|Logs Activity| G
    C2 -->|Logs Activity| G
    G -->|Streams to| H
    H -->|Protected by| I
    
    %% Security Monitoring
    C1 -->|Scanned by| J
    C2 -->|Scanned by| J
    J -->|Findings to| K
    K -->|Alerts to| L
    L -->|Notifies| M
    
    %% Operational Monitoring
    G -->|Metrics to| N
    N -->|Critical Alerts| M
    
    %% Subgraph styling
    style A fill:#4A90E2,stroke:#6DB3F2,stroke-width:3px
    style B fill:#9B59B6,stroke:#BB8FCE,stroke-width:3px
```
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

### 📦 JSON Stack #1 – Stand Alone S3 Replica Bucket:

**Description:**  

This CloudFormation template provisions a secure secondary-region S3 replica bucket with Object Lock (WORM), versioning, and KMS encryption to serve as a protected replication destination. It enforces private access, immutable storage, and controlled retention, making it suitable for disaster recovery, ransomware resilience, and compliance-driven data replication.

**Stack Diagram:**  

<img width="7369" height="3687" alt="s3_replica" src="https://github.com/user-attachments/assets/f4137035-ca09-4660-ade6-fe2060edefdd" />


---

### 📦 JSON Stack #2 - Parent Stack:

**Description:**  
Deploys additional region-specific S3 buckets configured for **CRR**, **Object Lock**, **Versioning**, and **KMS encryption**.

**Stack Diagram:**  



---

### 📦 JSON Stack #3 – Centralized Logging bucket:

**Description:**  
Centralized Logging CloudFormation Stack:
This CloudFormation template deploys a hardened S3 logging bucket with Object Lock (WORM), versioning, and KMS encryption to securely store S3 access logs and CloudTrail events. It enforces private, immutable log retention and integrates with CloudTrail and CloudWatch Logs, providing a tamper-resistant audit trail for security monitoring, forensics, and compliance.

**Stack Diagram:**  


<img width="7936" height="6892" alt="s3_logging_bucket" src="https://github.com/user-attachments/assets/827e7037-8502-4736-9ad0-a42d0772e0a2" />

---

### 📦 JSON Stack #4 - Main S3 Bucket:

**Description:**  

**Stack Diagram:**  
<img width="9064" height="8863" alt="s3_main_bucket" src="https://github.com/user-attachments/assets/15418642-2431-40a7-8b5b-bb966b799cae" />

---

### 📦 JSON Stack #5 - S3 MRAP:

**Description:**  

**Stack Diagram:**  
<img width="6847" height="3381" alt="s3_mrap" src="https://github.com/user-attachments/assets/42250329-de93-4d6d-a79a-1fad6478bf65" />

---

### 📦 JSON Stack #6 - Eventbridge, Macie & SNS:

**Description:**  

**Stack Diagram:**  
<img width="6841" height="5709" alt="s3_event_macie_sns" src="https://github.com/user-attachments/assets/f0a91131-731f-401f-8649-b7c73ab4edbf" />

---

### 📦 [JSON Stack #7 - CloudTrail Audit Logging:](stack_7_cloudtrail)
**Description:**  

**Stack Diagram:**  
<img width="6379" height="5194" alt="s3_cloudtrail" src="https://github.com/user-attachments/assets/02cc4028-1512-4b8d-9317-76942578b895" />

---

### 📦 JSON Stack #8 OPTIONAL - Config for Intelligent-Tiering:

**Description:**  

**Stack Diagram:**  

---

## ✅ Use Cases

- Ransomware-resistant backups
- Compliance-driven storage (SEC 17a-4, HIPAA, GDPR)
- Global application data access
- Forensics & audit readiness
- Zero-trust cloud architectures

---

## 🛡️ Deployment Script:  



---

## ⚠️ Important Post-Deployment

After parent stack deployment:

- ✅ Confirm email subscription (Stack 6)
- ✅ Update Replica Stack (Stack 1) with ReplicationRole ARN
- ✅ Test CloudTrail
- ✅ Test monitoring alerts

---

## 🛡️ Update Post-Deployment Script:  

