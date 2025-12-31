# 🌍 Secure Multi-Region S3 Architecture  
### Cross-Region Replication & Multi-Region Access Points 

![AWS](https://img.shields.io/badge/AWS-S3-orange)
![Security](https://img.shields.io/badge/Security-High-green)
![Availability](https://img.shields.io/badge/Availability-Multi--Region-blue)
![Encryption](https://img.shields.io/badge/Encryption-KMS-yellow)
![Compliance](https://img.shields.io/badge/Compliance-Ready-success)

---

# 📑 Table of Contents

- [Description](#description)
- [Architecture at a Glance](#architecture)
- [Security & Resilience Highlights](#security)
- [CloudFormation Stacks](#cloudformation-stacks)
  - [JSON Stack #1](#json-stack-1)
  - [JSON Stack #2](#json-stack-2)
  - [JSON Stack #3](#json-stack-3)

  
---

## 🧭 Description

This project implements a secure and resilient Amazon S3 solution featuring KMS-encrypted buckets with Object Lock and versioning to prevent data loss or tampering. Access is tightly controlled using least-privilege IAM roles, and all activity is captured in a restricted, immutable logging bucket for auditing. With built-in S3 replication and CloudWatch monitoring for access-denied events, the architecture creates a high-availability, disaster recovery, and ransomware-resistant design optimized for global access, durability, and security.
---

## 🏗️ Architecture at a Glance <a id="architecture"></a>

| Tools | Description |
|---------|------------|
| 🪣 **S3 Buckets** | Three buckets deployed across separate AWS regions for high availability and failover |
| 🌐 **Cross-Region Replication (CRR)** | Automatic replication of objects and object versions across regions |
| 🚀 **Multi-Region Access Points (MRAP)** | Global read/write access to the closest available S3 bucket |
| 🔐 **AWS KMS (customer-managed keys)** | Customer-managed KMS keys per region for encryption at rest |
| 🧱 **S3 Object Lock (immutable storage)** | Write-once, read-many (WORM) protection to prevent deletion or modification |
| 🔄 **S3 Object Versioning** | Preserves multiple versions of objects for recovery and rollback |
| 📊 **Amazon CloudWatch Alerts** | Monitoring and alerts for bucket activity, errors, and security events |
| 🧾 **IAM Policies & Roles** | Least-privilege access control for S3, KMS, replication, and logging |
| 🕵️ **Amazon Macie** | Automated discovery and classification of sensitive data in S3 |

### Architecture Diagram: 

---

## 🔐 Security & Resilience Highlights <a id="security"></a>

| Tool / Control                           | MITRE ATT&CK Technique    | Technique ID | How It Helps                                                 |
| ---------------------------------------- | ------------------------- | ------------ | ------------------------------------------------------------ |
| 🪣 **S3 Buckets (multi-region)**         | Data from Cloud Storage   | T1530        | Protects against data loss by spreading data across regions  |
| 🌐 **Cross-Region Replication (CRR)**    | Data Encrypted for Impact | T1486        | Ensures data survives ransomware or destructive attacks      |
| 🚀 **Multi-Region Access Points (MRAP)** | Network Service Discovery | T1046        | Reduces attack impact by routing users to healthy regions    |
| 🔐 **AWS KMS (CMKs)**                    | Unsecured Credentials     | T1552        | Prevents attackers from reading stolen data at rest          |
| 🧱 **S3 Object Lock (WORM)**             | Inhibit System Recovery   | T1490        | Stops attackers from deleting or overwriting backups         |
| 🔄 **S3 Object Versioning**              | Data Destruction          | T1485        | Enables recovery of deleted or altered objects               |
| 📊 **CloudWatch Alerts**                 | Account Manipulation      | T1098        | Detects abnormal API activity and permission changes         |
| 🧾 **IAM Policies & Roles**              | Abuse of Valid Accounts   | T1078        | Limits attacker impact through least-privilege access        |
| 🕵️ **Amazon Macie**                     | Data from Cloud Storage   | T1530        | Detects sensitive data exposure and misconfigurations        |

 

---

## CloudFormation Stacks

### [JSON Stack #1](S3_Bucket_CFN_JSON)

#### Description:
This CloudFormation stack implements a secure Amazon S3 storage by enabling Object Lock and Versioning to protect data from deletion or modification, using customer-managed AWS KMS keys for strong encryption, and enforcing least-privilege access through IAM roles, policies, and conditions. A separate, hardened logging bucket is included to securely store audit logs. This design helps protect sensitive data, supports compliance requirements, and improves resilience against accidental or malicious actions.

#### Stack Diagram:
<img width="7476" height="2709" alt="s3_Initial_Infrastructure" src="https://github.com/user-attachments/assets/7ed31e1a-8a34-4078-b196-5568d95af701" />

---
### [JSON Stack #2](s3_bucket_region_2)

#### Description:
This CloudFormation stack deploys a secure, versioned S3 bucket with Object Lock and KMS encryption; reusable across regions for cross-region replication (CRR).

#### Stack Diagram:
<img width="6484" height="544" alt="s3_Replicate_Bucket" src="https://github.com/user-attachments/assets/3c3cbc19-6458-4f31-91bf-12af5f1bedba" />

---

### [JSON Stack #3](S3_CRR_MRAP)

#### Description:
This CloudFormation template enables S3 Cross-Region Replication (CRR) to automatically replicate objects across multiple buckets in different regions and creates a Multi-Region Access Point (MRAP) for unified access. This ensures high availability, disaster recovery readiness, and global data accessibility while maintaining strong encryption on replicated objects. It helps organizations protect critical data, meet compliance requirements, and simplify cross-region data management in AWS.

#### Stack Diagram:
<img width="6228" height="591" alt="s3_CRR_MRAP" src="https://github.com/user-attachments/assets/7a45a333-933d-4f08-818f-2e662164d3f0" />


