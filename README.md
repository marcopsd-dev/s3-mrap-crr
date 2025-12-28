# 🌍 Secure Multi-Region S3 Architecture  
### Cross-Region Replication & Multi-Region Access Points 

![AWS](https://img.shields.io/badge/AWS-S3-orange)
![Security](https://img.shields.io/badge/Security-High-green)
![Availability](https://img.shields.io/badge/Availability-Multi--Region-blue)
![Encryption](https://img.shields.io/badge/Encryption-KMS-yellow)
![Compliance](https://img.shields.io/badge/Compliance-Ready-success)

---

# 📑 Table of Contents

- [Description](#-description)
- [Architecture at a Glance](Architecture-at-a-Glance)
- [Security & Resilience Highlights](#-security--resilience-highlights)
- [ JSON CloudFormation Code ](JSON-CloudFormation-Code)
- [GUI Console Use](GUI-Console-Use)

  
---

## 🧭 Description

This project demonstrates a **production-grade, highly available, fail-over, and secure AWS S3 architecture** designed for **global access, data durability, and ransomware resilience**.

---

## 🏗️ Architecture at a Glance

| Tools | Description |
|---------|------------|
| 🪣 **S3 Buckets** | Three buckets deployed across separate AWS regions for high availibility, fail-over, and  |
| 🌐 **Cross-Region Replication (CRR)** | Automatic duplication of objects stored in S3, and object versioning |
| 🚀 **Multi-Region Access Points (MRAP)** | Global read/write access via MRAP |
| 🔐 **AWS KMS (customer-managed keys)**| Customer-managed KMS keys per region |
| 🧱 **S3 Object Lock (immutable storage)**| Object Lock enabled for protection (immutability) |

---

## 🔐 Security & Resilience Highlights

✅ **Encryption at Rest**  
- All objects encrypted using **AWS KMS (CMKs)**  

✅ **Ransomware Protection**  
- **S3 Object Lock** prevents deletion or modification  

✅ **Least-Privilege Access**  
- IAM-controlled replication roles  

✅ **Disaster Recovery Ready**  
- Multi-region data durability and availability  

---

## JSON CloudFormation Code


---

## GUI Console Use
