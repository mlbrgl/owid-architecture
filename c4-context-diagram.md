<p><a target="_blank" href="https://app.eraser.io/workspace/nTub7lm1fB4TLlsFpql0" id="edit-in-eraser-github-link"><img alt="Edit in Eraser" src="https://firebasestorage.googleapis.com/v0/b/second-petal-295822.appspot.com/o/images%2Fgithub%2FOpen%20in%20Eraser.svg?alt=media&amp;token=968381c8-a7e7-472a-8ed6-4a6626da5501"></a></p>



# C4 Architecture Diagrams - Our World in Data Platform
![Figure 1](/.eraser/nTub7lm1fB4TLlsFpql0___skhqbyhYlBX0xs2EX2FVxLhSbiB3___---figure---HoejLG4EvJDvlSb4TXrTE---figure---me2ubT6UNVGLy_9lthvVbQ.png "Figure 1")

## System Context Diagram - OWID Platform
This diagram shows the OWID platform and its relationships with people and external systems.

[﻿Demo cloud diagram](https://app.eraser.io/workspace/sirBEZn7DRXwEkmGU253) 

```
Git users [icon: users]
Third-party Git repository [icon: git]

AWS Cloud [icon: aws] {
  Region [icon: flag] {
    Amazon API Gateway [icon: aws-api-gateway]
    VPC [icon: aws-vpc] {
      Private subnet [icon: aws-private-subnet] {
        Lambda function [icon: aws-lambda]
        AWS CodeBuild [icon: aws-codebuild]
      }
    }
    Amazon S3 SSH key bucket [icon: aws-s3]
    AWS KMS key [icon: key]
    Amazon S3 output bucket [icon: aws-s3]
  }
}

Git users > Third-party Git repository > Amazon API Gateway > Lambda function > AWS CodeBuild > AWS KMS key
AWS CodeBuild > Third-party Git repository
AWS CodeBuild > Amazon S3 output bucket, Amazon S3 SSH key bucket
```
```mermaid
C4Context
title System Context - Our World in Data Platform

Person(public_user, "Public User", "Reads articles, explores data visualizations")
Person(content_author, "Content Author", "Writes articles in Google Docs using ArchieML")
Person(data_analyst, "Data Analyst", "Creates and configures charts, uploads data")

System(owid_platform, "OWID Platform", "Data journalism platform with interactive visualizations")

System_Ext(google_docs, "Google Docs", "Content authoring with ArchieML markup")
System_Ext(mysql, "MySQL Database", "Persistent data storage")
System_Ext(cloudflare_r2, "Cloudflare R2", "Static asset storage and CDN")
System_Ext(stripe, "Stripe", "Payment processing for donations")
System_Ext(email_service, "Email Service", "Transactional emails")
System_Ext(cloudflare_edge, "Cloudflare Workers", "Edge computing platform")

Rel(public_user, owid_platform, "Views articles and charts", "HTTPS")
Rel(public_user, owid_platform, "Makes donations", "HTTPS")

Rel(content_author, google_docs, "Writes content using ArchieML", "HTTPS")
Rel(data_analyst, owid_platform, "Manages charts and data", "HTTPS")

Rel(owid_platform, google_docs, "Fetches articles via API", "HTTPS/REST")
Rel(owid_platform, mysql, "Stores/retrieves data", "MySQL Protocol")
Rel(owid_platform, cloudflare_r2, "Stores/serves static assets", "S3 API")
Rel(owid_platform, stripe, "Processes donations", "HTTPS/REST")
Rel(owid_platform, email_service, "Sends notifications", "SMTP")

Rel(cloudflare_edge, owid_platform, "Requests dynamic content", "HTTPS")
Rel(cloudflare_edge, cloudflare_r2, "Serves static HTML/assets", "S3 API")
Rel(public_user, cloudflare_edge, "Accesses site", "HTTPS")

UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```
**Legend:**

- **Person** (shown as stick figure): Human users of the system
- **System** (blue box): The OWID platform itself
- **External System** (gray box): External systems the platform integrates with
- **Relationship** (arrows): Labeled with purpose and protocol
**Key Points:**

- The OWID platform serves two primary user groups: public users (readers) and internal users (authors/analysts)
- Content is authored externally in Google Docs using ArchieML markup
- Static content is served via Cloudflare's edge network for performance
- The platform integrates with multiple external services for specialized functionality



<!-- eraser-additional-content -->
## Diagrams
<!-- eraser-additional-files -->
<a href="/c4-context-diagram-entity-relationship-1.eraserdiagram" data-element-id="vc7gFjBMM42vEU6Kk62fM"><img src="/.eraser/nTub7lm1fB4TLlsFpql0___skhqbyhYlBX0xs2EX2FVxLhSbiB3___---diagram----19ab055a129fc094491a5695c63657a0.png" alt="" data-element-id="vc7gFjBMM42vEU6Kk62fM" /></a>
<a href="/c4-context-diagram-cloud-architecture-2.eraserdiagram" data-element-id="XL1k9YKWD7afWLJk_YC74"><img src="/.eraser/nTub7lm1fB4TLlsFpql0___skhqbyhYlBX0xs2EX2FVxLhSbiB3___---diagram----f96fb10d4a22d5c52b28d93e83da0b20.png" alt="" data-element-id="XL1k9YKWD7afWLJk_YC74" /></a>
<!-- end-eraser-additional-files -->
<!-- end-eraser-additional-content -->
<!--- Eraser file: https://app.eraser.io/workspace/nTub7lm1fB4TLlsFpql0 --->