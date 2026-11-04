# CloudNova — Serverless Resume Website

A responsive resume and portfolio website built with **HTML, CSS, JavaScript, and AWS serverless services**. The project combines static website hosting, a serverless visitor counter, and automated deployment through GitHub Actions.

## Overview

CloudNova presents my professional profile, technical skills, projects, and contact information. A visitor counter demonstrates an event-driven serverless backend using API Gateway, Lambda, and DynamoDB.

## Deployment Status

The website was previously deployed using Amazon S3 and CloudFront. The AWS hosting resources have since been decommissioned to avoid ongoing charges, so the live demo link is currently unavailable. The repository and screenshots document the project.

## Screenshot

<img width="222" height="448" alt="CloudNova resume website screenshot" src="https://github.com/user-attachments/assets/5f341a1b-6ac0-42fe-b44e-0952d4281518" />

## Features

- Responsive resume and portfolio layout
- Sections for profile, skills, projects, and contact information
- Dynamic visitor count retrieved from an API
- Serverless backend for updating and storing the visitor count
- Automated website deployment using GitHub Actions

## AWS Architecture

### Website Hosting

1. **Amazon S3** — stores the website’s static files
2. **Amazon CloudFront** — delivers the website through a content delivery network (CDN)

### Visitor Counter

1. **Amazon API Gateway (HTTP API)** — exposes the visitor counter endpoint
2. **AWS Lambda** — processes visitor count requests
3. **Amazon DynamoDB** — stores the visitor count

The website requests the visitor count from API Gateway. API Gateway invokes Lambda, which updates the count in DynamoDB and returns the latest value to the website.

## CI/CD Workflow

1. Code changes are pushed to the GitHub repository.
2. GitHub Actions authenticates with AWS using OpenID Connect (OIDC).
3. The workflow deploys the website files to Amazon S3.
4. Amazon CloudFront delivers the updated website.

## Testing & Results

- **100/100 successful API responses** in a 100-request test (100% success rate).
- **204 ms average response time** across the 100-request latency test.
- **100/100 successful responses** in a test of 100 requests using up to 10 concurrent workers (100% success rate).

*These are results from controlled tests, not a guarantee of production uptime or capacity.*

## Tech Stack

- HTML, CSS, JavaScript
- Amazon S3 and Amazon CloudFront
- Amazon API Gateway (HTTP API)
- AWS Lambda (Python)
- Amazon DynamoDB
- GitHub Actions
- AWS IAM with OpenID Connect (OIDC)

## Repository Structure

```text
CloudNova-Serverless-Resume/
├── index.html
├── styles.css
└── README.md
```
