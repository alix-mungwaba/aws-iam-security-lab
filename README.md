# AWS IAM Security & Access Control Lab

![AWS](https://img.shields.io/badge/AWS-IAM%20%7C%20S3%20%7C%20CloudTrail-232F3E?style=flat&logo=amazon-aws)
![Security](https://img.shields.io/badge/Security-Least%20Privilege%20%7C%20MFA-red)

A hands-on cloud security lab demonstrating IAM user/group management, least privilege access control, custom JSON policies, MFA enforcement, and CloudTrail auditing.

---

## ⚡ Quick Summary
- **Least Privilege:** Analyst1 restricted to read-only S3 actions; write/delete attempts blocked.
- **MFA:** Enabled on AdminUser to secure high-privilege access.
- **Audit:** CloudTrail logs confirmed denied `s3:PutObject` and `s3:CreateBucket` events.

---
## 🧩 Skills Demonstrated

- IAM User & Group Management
- Least Privilege Access Control
- Custom JSON Policy Design
- MFA Configuration
- CloudTrail Security Auditing
---

## 🛠️ Tools Used
`AWS IAM` • `Amazon S3` • `AWS CloudTrail` • `JSON`

---

## 📸 Proof of Concept

| Analyst Access Denied | Admin Access Granted |
| :---: | :---: |
| <img width="1871" height="962" alt="Screenshot 2026-08-05 154002" src="https://github.com/user-attachments/assets/e9b8cc65-8362-41c5-8dd3-ba04901edece" /> | <img width="1897" height="975" alt="Screenshot 2026-08-05 154313" src="https://github.com/user-attachments/assets/4fcfdc7c-11b0-4f5c-a751-f09c6f386c38" /> 


| Custom JSON Policy | CloudTrail Logs |
| :---: | :---: |
| <img width="1872" height="988" alt="Screenshot 2026-08-05 171002" src="https://github.com/user-attachments/assets/31f9ecf3-3bd5-4fa8-b288-24c8a8aa76df" /> | <img width="1882" height="977" alt="Screenshot 2026-08-05 181022" src="https://github.com/user-attachments/assets/2fc31141-d38b-42ed-91d2-3f70efbb817c" />

---

<details>
<summary>🔍 <b>Click to expand full step-by-step implementation details</b></summary>

<br>

## 1. IAM Users & Groups

### Users
- **AdminUser:** Full admin access + MFA  
- **Analyst1:** Read-only S3 access

### Groups
- **AdminGroup:** AWS-managed `AdministratorAccess`  
- **ReadOnlyGroup:** Custom S3 read-only policy

| AdminUser Overview | AdminGroup Permissions |
| :---: | :---: |
| <img width="1861" height="952" alt="Screenshot 2026-08-05 012948" src="https://github.com/user-attachments/assets/caa2fa09-3488-4732-a56d-d214146000c3" /> | <img width="1862" height="951" alt="Screenshot 2026-08-05 013138" src="https://github.com/user-attachments/assets/4fc80351-8674-4526-a88c-fa98c18c35e1" />


| Analyst1 Overview | ReadOnlyGroup Permissions |
| :---: | :---: |
| <img width="1868" height="958" alt="Screenshot 2026-08-05 013007" src="https://github.com/user-attachments/assets/c184121e-09b9-415d-a660-e9bef0e93d29" /> |<img width="1862" height="957" alt="Screenshot 2026-08-05 013115" src="https://github.com/user-attachments/assets/75a75e22-1b0f-4c4b-817b-ef81c4e95c1f" />


---

## 2. Custom JSON Policy (Least Privilege)

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Allow",
      "Action": [
        "s3:ListAllMyBuckets",
        "s3:ListBucket",
        "s3:GetObject"
      ],
      "Resource": "*"
    }
  ]
}
