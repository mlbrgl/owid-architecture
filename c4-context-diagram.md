# C4 Architecture Diagrams - Our World in Data Platform

## System Context Diagram - OWID Platform

This diagram shows the OWID platform and its relationships with people and external systems.

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
