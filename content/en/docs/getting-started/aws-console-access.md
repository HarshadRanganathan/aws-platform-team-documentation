---
title: "AWS Console Access"
description: ""
lead: ""
date: 2022-01-14T00:14:16Z
lastmod: 2022-01-14T00:14:16Z
draft: false
images: []
menu: 
  docs:
    parent: "getting-started"
weight: 1
toc: true
---

## Console URL

We use SAML based federated login.

1. Bookmark this console URL

2. On Successful login, select the role that you want to assume. Your permissions will vary based on the role assumed.

## Roles

Below are the roles available.

Please raise request to the appropriate role that you need.

{{<alert icon="⚠️" text="Only request the least privilege role that you need" />}}

|Account |Role |Targeted Users|
|--|--|--|
|Non-Prod |AWS_xxxxx_Read |PO |
|Non-Prod |AWS_xxxxx_Contributor |Developers |
|Non-Prod |AWS_xxxxx_Owner |Infrastructure Team |

<div class="alert alert-light" role="alert">
  <h4 class="alert-heading">Contributor Role Restrictions</h4>
  <p>Following actions are denied in the contributor role:</p>
  <p>❌ IAM Create/Update/Delete</p>
  <p>❌ RDS DB Deletion</p>
  <p>❌ MSK Cluster deletion</p>
  <p>❌ Elasticsearch deletion</p>
  <p>❌ EKS Deletion</p>
  <p>❌ EKS Upgrades</p>
  <p>❌ S3 bucket deletion</p>
  <p>❌ Lambda deletion</p>
  <p>❌ RDS DB Proxy deletion</p>
  <p>❌ Route53 deletion</p>
  <p>❌ VPC deletion</p>
  <p>❌ Security Groups deletion</p>
  <p>❌ Step Functions deletion</p>
  <p>❌ API Gateway deletion</p>
  <p>❌ Cloudfront deletion</p>
  <p>❌ WAF deletion</p>
  <p>❌ Cloudwatch Events deletion</p>
</div>

## Session Timeout

When your session times out, you will get below error:

{{<alert icon="⚠️" text="There was a problem with your session. To start a new session return to the link provided by your administrator<br/><br/>To logout, click here" />}}

Or you may re-directed to an alternative AWS customer sign-in screen.

Do not use the customer AWS sign-in screen, instead use the SAML federated link to login again.
