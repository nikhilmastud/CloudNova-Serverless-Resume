# CloudNova — Serverless Resume Website

A personal resume and portfolio website built with **HTML, CSS, JavaScript, and AWS serverless services**.

## Overview

CloudNova presents my professional profile, technical skills, and projects in a responsive portfolio website. It also includes a visitor counter powered by AWS services.

## Features

- Responsive resume and portfolio layout
- Sections for profile, skills, projects, and contact information
- Dynamic visitor count retrieved from an API
- Serverless backend for updating and storing visitor count

## AWS Architecture

1. **Amazon S3** — stores the website’s static files
2. **Amazon API Gateway (HTTP API)** — exposes the visitor counter endpoint
3. **AWS Lambda** — processes visitor count requests
4. **Amazon DynamoDB** — stores the visitor count

The website requests the visitor count from API Gateway. API Gateway invokes Lambda, which updates the count in DynamoDB and returns the latest value to the website.

## Tech Stack

- HTML
- CSS
- JavaScript
- Amazon S3
- Amazon API Gateway
- AWS Lambda (Python)
- Amazon DynamoDB

## Repository Structure

```text
CloudNova-Serverless-Resume/
├── index.html
├── styles.css
├── script.js
└── README.md
```

## Run Locally

1. Clone the repository:
   ```bash
   git clone https://github.com/nikhilmastud/CloudNova-Serverless-Resume.git
   ```
2. Open the project folder in VS Code.
3. Run `index.html` using Live Server.

The visitor counter requires the AWS API endpoint to be available.

## Project Status

The S3 website files and visitor counter backend have been configured. CloudFront distribution setup is pending AWS account verification.

## Author

**Nikhil Mastud**

- GitHub: [nikhilmastud](https://github.com/nikhilmastud)
