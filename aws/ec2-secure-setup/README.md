# Secure EC2 Setup with CloudTrail Logging

## Summary
This lab deploys an EC2 instance in a public subnet with:
- A Security Group restricting SSH access to **my IP only**.
- CloudTrail logging all actions to an encrypted S3 bucket.
- Public access to S3 blocked to prevent accidental exposure.

## Architecture
```mermaid
flowchart LR
    User((My IP)) -->|SSH| SG[Security Group]
    SG --> EC2[EC2 t2.micro]
    EC2 -->|API Calls| CloudTrail
    CloudTrail --> S3[(S3 Log Bucket)]
    subgraph VPC
        SG
        EC2
    end

