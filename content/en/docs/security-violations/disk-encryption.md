---
title: "Disk Encryption"
description: ""
lead: ""
date: 2022-07-22T12:54:40+01:00
lastmod: 2022-07-22T12:54:40+01:00
draft: false
images: []
menu: 
  docs:
    parent: "security-violations"
weight: 2
toc: true
---

## EMR

To encrypt the disk for EMR workloads, perform following actions:

[1] Create a new CMK KMS key to be used for encryption with below policy (substituting with your account id):

```json
{
    "Id": "encryption-policy",
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::<account-id>:root"
            },
            "Action": "kms:*",
            "Resource": "*"
        },
        {
            "Sid": "Allow use of the key",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::<account-id>:role/EMR_EC2_DefaultRole"
                ]
            },
            "Action": [
                "kms:Encrypt",
                "kms:Decrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey"
            ],
            "Resource": "*"
        },
        {
            "Sid": "Allow attachment of persistent resources",
            "Effect": "Allow",
            "Principal": {
                "AWS": [
                    "arn:aws:iam::<account-id>:role/EMR_EC2_DefaultRole"
                ]
            },
            "Action": [
                "kms:CreateGrant",
                "kms:ListGrants",
                "kms:RevokeGrant"
            ],
            "Resource": "*",
            "Condition": {
                "Bool": {
                    "kms:GrantIsForAWSResource": "true"
                }
            }
        }
    ]
}
```

[2] Create a new EMR security configuration with below configuration (substitute with kms key you had created previously):

```json

   
{
  "EncryptionConfiguration": {
    "EnableInTransitEncryption": false,
    "EnableAtRestEncryption": true,
    "AtRestEncryptionConfiguration": {
      "S3EncryptionConfiguration": {
        "EncryptionMode": "SSE-S3"
      },
      
      "LocalDiskEncryptionConfiguration": {
        "EncryptionKeyProviderType": "AwsKms",
        "AwsKmsKey": "<kms-arn>"
      }
    }
  }, 
  "InstanceMetadataServiceConfiguration" : {
      "MinimumInstanceMetadataServiceVersion": 2,
      "HttpPutResponseHopLimit":1
  }
}
```

[3] Configure your EMR workloads to use the new security configuration from previous step.
