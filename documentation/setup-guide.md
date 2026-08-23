# AWS S3 IAM Access Control Setup Guide

## 1. Introduction

This guide explains the setup process for implementing user-based access control using Amazon S3 and AWS IAM policies.

The project creates a shared S3 bucket where:

- Smriti can read and write inside her own folder.
- Smriti can only read Palak's folder.
- Palak can read and write inside her own folder.
- Palak can only read Smriti's folder.

---

## 2. AWS S3 Bucket Creation

### Step 1: Create S3 Bucket

1. Open AWS Management Console.

2. Navigate to:

```
S3 → Create Bucket
```

3. Enter bucket name:

```
smriti-aws-access-control
```

4. Select the required AWS Region.

5. Keep public access blocked:

```
Block Public Access: Enabled
```

6. Create the bucket.

---

## 3. Creating Folder Structure

Inside the S3 bucket, create the following folders:

```
smriti/
palak/
```

Final structure:

```
smriti-aws-access-control

│
├── smriti/
│
└── palak/
```

---

## 4. Creating IAM Users

Navigate to:

```
AWS Console → IAM → Users → Create User
```

Create two IAM users:

```
smriti-user
palak-user
```

Generate access keys if AWS CLI testing is required.

---

## 5. IAM Policy Configuration

## Smriti User Policy

Smriti user has complete access to her own folder.

Allowed permissions:

```
s3:GetObject
s3:PutObject
s3:DeleteObject
```

Resource:

```
smriti/*
```

Smriti also has read-only access to Palak's folder.

Allowed permission:

```
s3:GetObject
```

Resource:

```
palak/*
```

---

## Palak User Policy

Palak user has complete access to her own folder.

Allowed permissions:

```
s3:GetObject
s3:PutObject
s3:DeleteObject
```

Resource:

```
palak/*
```

Palak also has read-only access to Smriti's folder.

Allowed permission:

```
s3:GetObject
```

Resource:

```
smriti/*
```

---

## 6. Attaching IAM Policies

Attach:

```
smriti-policy.json
```

to:

```
smriti-user
```

Attach:

```
palak-policy.json
```

to:

```
palak-user
```

---

## 7. Testing Permissions

Permissions can be tested using AWS CLI.

### Smriti User Testing

### Upload file to own folder

Command:

```bash
aws s3 cp test.txt s3://smriti-aws-access-control/smriti/
```

Expected Result:

```
Upload successful
```

---

### Upload file to Palak's folder

Command:

```bash
aws s3 cp test.txt s3://smriti-aws-access-control/palak/
```

Expected Result:

```
Access Denied
```

---

### Read Palak's folder

Command:

```bash
aws s3 ls s3://smriti-aws-access-control/palak/
```

Expected Result:

```
Files visible
```

---

## 8. Security Principles Implemented

This project demonstrates:

- Identity and Access Management (IAM)
- Least Privilege Access Control
- S3 Object-Level Permissions
- Secure Cloud Storage
- User-Based Authorization

---

## 9. Conclusion

AWS S3 combined with IAM policies provides secure and controlled access to cloud storage.

By applying different permissions for different users, collaboration can be achieved while preventing unauthorized modification of data.