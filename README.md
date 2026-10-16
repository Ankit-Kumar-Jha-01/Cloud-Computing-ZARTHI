# AWS S3 Static Website Hosting & Cloud Architecture

A responsive static personal portfolio website hosted on Amazon Web Services (AWS) using S3. This repository contains the source code (HTML5, CSS3), cloud infrastructure configuration details, bucket permissions setup, and troubleshooting documentation for static site hosting.

---

## 📌 Project Architecture

```text
[ User / Web Browser ]
         │
         │ (HTTP GET Requests)
         ▼
 ┌─────────────────────────────────────────────────────────┐
 │ AWS S3 Bucket (Static Website Hosting)                 │
 │  ├── index.html                                        │
 │  ├── about.html                                        │
 │  ├── contact_us.html                                   │
 │  ├── style.css                                         │
 │  └── me.jpeg                                           │
 └─────────────────────────────────────────────────────────┘
         │
         │ (Access Request Logs)
         ▼
 ┌─────────────────────────────────────────────────────────┐
 │ AWS Target S3 Log Bucket (Server Access Logging)        │
 └─────────────────────────────────────────────────────────┘
```

* **AWS S3 (Simple Storage Service):** Primary cloud storage layer serving as the public web root for HTML, CSS, and media assets.
* **S3 Server Access Logging:** Independent bucket target configured to capture real-time HTTP request metrics, timestamps, and caller details.
* **S3 Bucket Versioning:** State preservation feature enabled to prevent accidental deletion and preserve deployment revisions.

---

## 📁 Repository Structure

```text
aws-s3-static-website/
├── index.html        # Main landing page featuring personal overview
├── about.html        # Learnings, cloud concepts, and technical reflections
├── contact_us.html  # Interactive contact details page
├── style.css         # Modular CSS stylesheets for layout & responsiveness
├── me.jpeg           # Profile image asset
└── README.md         # Full project technical documentation
```

---

## 🛠️ Step-by-Step AWS Setup & Deployment

### 1. Bucket Creation & File Upload
1. Log in to the **AWS Management Console** and navigate to **S3**.
2. Select **Create bucket**, choose your region (e.g., `eu-north-1`), and assign a globally unique bucket name.
3. Upload all root project files (`index.html`, `about.html`, `contact_us.html`, `style.css`, and `me.jpeg`).

### 2. Static Website Hosting Configuration
1. Open the bucket **Properties** tab.
2. Scroll to **Static website hosting** and select **Edit**.
3. Set **Static website hosting** to *Enable*.
4. Specify `index.html` as the **Index document** and save changes.

### 3. Public Permissions & Security Configuration
1. Navigate to the **Permissions** tab.
2. Under **Block public access (bucket settings)**, click **Edit**, uncheck **Block *all* public access**, and confirm changes.
3. Scroll down to **Bucket policy**, click **Edit**, and paste the following JSON policy to allow public read-only access (`s3:GetObject`):

```json architecture
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```


### 4. Logging & Versioning Enablement
1. In **Properties**, enable **Bucket Versioning** to maintain historical states of uploaded objects.
2. Under **Server access logging**, choose **Enable** and set a dedicated destination log bucket (e.g., `s3://your-log-bucket-name/`) to prevent recursive logging loops.

---

## ⚡ Technical Challenges & Solutions

| Issue / Error | Root Cause | Resolution |
| :--- | :--- | :--- |
| **HTTP 403 Forbidden** | Default AWS security settings block all incoming unauthenticated public requests to S3 objects. | Disabled "Block Public Access" and attached a public `s3:GetObject` JSON bucket policy. |
| **Access Logs Not Appearing Immediately** | AWS S3 buffers server logs internally before writing them to the logging target bucket. | Confirmed via AWS documentation that log propagation requires a few minutes to reflect in the target bucket. |
| **Mobile Web Browser Warnings** | S3 default website endpoints operate over plain `http://` rather than encrypted `https://`. | Documented HTTP security restrictions on mobile devices (*Next Step: Route traffic through AWS CloudFront with SSL/TLS*). |

---


## 🎯 Future Enhancements

* **AWS CloudFront Integration:** Place a CloudFront Content Delivery Network (CDN) in front of S3 for edge caching and SSL/TLS HTTPS encryption.
* **Custom Domain Mapping:** Use AWS Route 53 to map a custom domain name to the CloudFront distribution.
* **CI/CD Pipeline:** Configure GitHub Actions to automatically sync changes to the S3 bucket on every `git push`.

---

## 👤 Author

* **Ankit Kumar Jha** - [GitHub Profile](https://github.com/Ankit-Kumar-Jha-01) | [LinkedIn](https://www.linkedin.com/in/ankit-kumar-jhaa)
