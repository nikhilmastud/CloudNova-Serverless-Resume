# CloudNova — Serverless Resume Website

A personal resume and portfolio website built with **HTML, CSS, JavaScript, and AWS serverless services**.

## Overview

CloudNova presents my professional profile, technical skills, and projects in a responsive portfolio website. It also includes a visitor counter powered by AWS services.

## Live Website

[View CloudNova Resume](https://d3ksbq7u0m2hj2.cloudfront.net)

<img width="222" height="448" alt="image" src="https://github.com/user-attachments/assets/5f341a1b-6ac0-42fe-b44e-0952d4281518" />


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

- HTML
- CSS
- JavaScript
- Amazon S3
- Amazon CloudFront
- Amazon API Gateway
- AWS Lambda (Python)
- Amazon DynamoDB
- GitHub Actions
- AWS IAM OIDC

## Repository Structure

```text
CloudNova-Serverless-Resume/
├── index.html
├── styles.css
└── README.md
```
