# aws-s3-access-control
Implementation of AWS S3 and IAM based access control with user-specific read and write permissions.

# AWS S3 IAM-Based Access Control System

## Project Overview

This project demonstrates the implementation of **secure file access control using Amazon S3 and AWS IAM policies**.

The objective is to create a shared cloud storage system where multiple users have different levels of permissions based on their assigned folders.

Each user can:
- Read and write files inside their own folder
- Read files from another user's folder
- Cannot modify or delete files belonging to another user

This project follows the **Principle of Least Privilege**, ensuring users only receive the permissions required for their tasks.

---

# Architecture
                     AWS Account

                          |
                          |

                Amazon S3 Bucket

          smriti-aws-access-control

                   /             \

              smriti/            palak/

                 |                  |

          Smriti IAM User     Palak IAM User

          Read + Write        Read + Write

          Own Folder          Own Folder


          Read Only           Read Only

          Palak Folder        Smriti Folder

---

# AWS Services Used

| AWS Service | Purpose |
|-------------|---------|
| Amazon S3 | Provides scalable cloud object storage |
| AWS IAM | Manages users and permissions |
| IAM Policies | Defines user-specific access rules |
| AWS CLI | Used for testing access permissions |

---

# Project Structure
ws-s3-access-control/

│
├── architecture/
│ └── architecture-diagram.png
│
├── documentation/
│ └── setup-guide.md
│
├── iam-policies/
│ ├── smriti-policy.json
│ └── palak-policy.json
│
├── screenshots/
│
├── README.md
│
└── LICENSE

---

# Access Control Requirements

The project implements the following permission model:

| User | Own Folder | Other User Folder |
|------|------------|------------------|
| Smriti | Read + Write | Read Only |
| Palak | Read + Write | Read Only |

---

# IAM Policy Implementation

## Smriti User Policy

Smriti has full access to her own folder.

Allowed operations:
s3:GetObject
s3:PutObject
s3:DeleteObject


Resource:


smriti/*


Smriti can also view files from Palak's folder.

Allowed operation:


s3:GetObject


Resource:


palak/*


---

## Palak User Policy

Palak has full access to her own folder.

Allowed operations:


s3:GetObject
s3:PutObject
s3:DeleteObject


Resource:


palak/*


Palak can also view files from Smriti's folder.

Allowed operation:


s3:GetObject


Resource:


smriti/*


---

# Security Concepts Implemented

This project demonstrates:

- Identity and Access Management (IAM)
- User-based access control
- Object-level permissions
- Least Privilege Security Model
- Secure cloud storage
- AWS S3 permission management

---

# Testing Access Permissions

Permissions are tested using AWS CLI commands.

## Upload File to Own Folder

Example:

```bash
aws s3 cp test.txt s3://bucket-name/smriti/

Result:

Access Allowed