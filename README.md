# 📸 Serverless Event-Driven Image Ingestion & Processing Pipeline

[![AWS](https://img.shields.io/badge/AWS-S3%20%7C%20Lambda%20%7C%20DynamoDB-orange?logo=amazon-aws)](https://aws.amazon.com/)
[![LocalStack](https://img.shields.io/badge/Emulation-LocalStack%203.8-blue?logo=docker)](https://localstack.cloud/)
[![Python](https://img.shields.io/badge/Language-Python%203.9-3776AB?logo=python)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Container-Docker%20Desktop-2496ED?logo=docker)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

An enterprise-ready, serverless event-driven media ingestion architecture. This project demonstrates asynchronous cloud processing: uploading media assets to Amazon S3, automatically triggering Python AWS Lambda microservices via S3 `ObjectCreated` events, indexing file metadata into Amazon DynamoDB, and outputting thumbnails to a processed storage tier.

---

## 🏛️ Architecture Diagram

```mermaid
flowchart LR
    User["👤 User / Mobile App"] -->|1. Upload Raw Image| S3_Raw["🪣 S3: Raw Uploads Bucket<br><i>raw-images-incoming-2026</i>"]
    S3_Raw -->|2. S3 ObjectCreated Event| Lambda["⚙️ AWS Lambda (Python 3.9)<br><i>ImageProcessorFunction</i>"]
    Lambda -->|3. Index Metadata| DynamoDB[("📊 DynamoDB: ImageCatalog<br><i>Item Details & Timestamps</i>")]
    Lambda -->|4. Generate Thumbnail| S3_Thumb["🪣 S3: Processed Thumbnails<br><i>processed-thumbnails-2026</i>"]
