# CloudNova — Architecture

The project is organized into three numbered stages. Follow the boxes **1 → 2 → 3**.

```mermaid
flowchart LR
    S1["<b>1 · HOST THE WEBSITE</b><br/><br/>Visitor opens site<br/>↓<br/>Amazon CloudFront<br/>↓<br/>Amazon S3<br/><i>Static resume files</i>"]
    S2["<b>2 · COUNT VISITORS</b><br/><br/>Website JavaScript<br/>↓ GET /visitors<br/>Amazon API Gateway<br/>↓<br/>AWS Lambda (Python)<br/>↓<br/>Amazon DynamoDB<br/><i>Increment and store count</i><br/><br/>Updated count returns to website"]
    S3["<b>3 · DEPLOY AUTOMATICALLY</b><br/><br/>GitHub push to main<br/>↓<br/>GitHub Actions<br/>↓ OIDC<br/>AWS IAM Role<br/>↓<br/>Deploy website files to S3"]

    S1 --> S2 --> S3

    classDef website fill:#EAF2FF,stroke:#2563EB,color:#12305A,stroke-width:2px;
    classDef counter fill:#F3E8FF,stroke:#7C3AED,color:#3B176B,stroke-width:2px;
    classDef deploy fill:#E8F7EC,stroke:#239447,color:#124B27,stroke-width:2px;

    class S1 website;
    class S2 counter;
    class S3 deploy;
```

## Request flow

1. CloudFront delivers the resume website files stored in S3.
2. The website calls API Gateway at `GET /visitors`.
3. API Gateway invokes the Python Lambda function.
4. Lambda increments the visitor count in DynamoDB.
5. The updated count returns to the website and is displayed.
6. GitHub Actions deploys website updates to S3 using AWS IAM OIDC authentication.
