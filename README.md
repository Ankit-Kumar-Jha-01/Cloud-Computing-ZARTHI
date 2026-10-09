# AWS S3 Static Website Hosting

A lightweight, hands-on cloud computing project demonstrating how to deploy, configure, and troubleshoot a static website hosted on **Amazon S3 (Simple Storage Service)**.

---

## 📌 Project Overview

This repository contains the source code and documentation for hosting a static web project on AWS S3. It demonstrates key cloud concepts including object storage, access policies, static web hosting, and access logging.

### Key Learnings & Architecture
* **Storage & Hosting:** Hosted HTML/CSS files directly on AWS S3 as an object storage service.
* **Access Control:** Configured S3 bucket permissions using JSON-based **Bucket Policies** (`s3:GetObject`) and managed S3 **Block Public Access** settings.
* **Troubleshooting:** Diagnosed and resolved standard HTTP `403 Forbidden` access issues.
* **Monitoring & Integrity:** Configured **Server Access Logging** to track requests and enabled **S3 Versioning** to protect against accidental file deletions.

---

## 📁 Repository Structure

```text
├── index.html        # Main landing page
├── about.html        # Project details and learnings
├── contact_us.html   # Contact information page
├── style.css         # Styling stylesheet for website layouts
├── me.jpeg           # Profile image asset
└── README.md         # Project documentation
```

---

## 🛠️ Step-by-Step Implementation

1. **Bucket Creation:** Created an AWS S3 bucket configured for general-purpose storage.
2. **File Upload:** Uploaded web assets (`index.html`, `about.html`, `contact_us.html`, `style.css`, and images)
