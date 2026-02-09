# AWS IAM Least Privilege Role + CloudTrail Audit Logging

## Goal
Implement a least-privilege IAM role for an EC2 service and enable CloudTrail to provide full visibility into IAM activity for auditing and incident response.

---

## Overview
This project demonstrates how to securely configure AWS Identity and Access Management (IAM) using the principle of least privilege and how to enable and verify CloudTrail audit logging. The focus is on reducing blast radius, eliminating long-lived credentials, and ensuring security events are captured and protected.

---

## What Was Configured

### IAM
- Created an **EC2 service role** (`EC2-LeastPrivilege-S3Role`)
- Attached a **customer-managed IAM policy** scoped to:
  - Read-only access
  - A **specific S3 bucket only**
- Avoided AWS-managed admin or full-access policies
- Used roles instead of users to prevent long-lived credentials

### CloudTrail
- Enabled a **multi-region CloudTrail** (`Security-Audit-Trail`)
- Configured centralized log storage in S3
- Enabled **log file validation** to detect tampering
- Enabled **SSE-KMS encryption** for audit log confidentiality
- Verified logging by reviewing IAM management events in Event History

---

## Why This Matters
- Least privilege limits damage if a service or credential is compromised
- IAM roles eliminate static access keys for AWS services
- CloudTrail provides accountability: *who did what, when, and from where*
- Log validation and encryption protect audit integrity and confidentiality
- These controls are foundational for SOC, cloud security, and compliance environments

---

## Evidence

### IAM Least-Privilege Role
![IAM Role](evidence/01-iam-role-least-privilege.png)

### CloudTrail Secure Configuration
![CloudTrail Config](evidence/02-cloudtrail-secure-config.png)

### IAM Activity Logged in CloudTrail
![IAM Events](evidence/03-cloudtrail-iam-event-history.png)

---

## Policy Files
- IAM policy enforcing scoped S3 read-only access:  
  `policies/s3-readonly-specific-bucket.json`

---

## Threats Mitigated
- Privilege escalation from over-permissioned IAM roles
- Unauthorized access due to long-lived credentials
- Undetected IAM changes without audit logging
- Audit log tampering without validation or encryption

---

## Key Takeaways
- IAM roles should be used for services, not users
- Permissions should always be scoped to the minimum required actions and resources
- CloudTrail should be enabled across all regions
- Audit logs should be encrypted and validated by default

---

## Interview Talking Points
- Difference between IAM users and roles
- Why least privilege reduces blast radius
- How CloudTrail supports auditing and incident response
- Importance of log integrity and encryption

---

## Next Steps
- Integrate CloudTrail logs with CloudWatch or a SIEM
- Add alerting for sensitive IAM actions
- Expand policy analysis using IAM Access Analyzer
