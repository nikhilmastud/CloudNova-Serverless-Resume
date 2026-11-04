# CloudNova Architecture Diagram

This diagram represents the deployed CloudNova serverless resume website and visitor counter.

```mermaid
flowchart LR
    U[Visitor / Browser]

    subgraph Hosting["Static Website Hosting"]
      CF[Amazon CloudFront]
      S3[(Amazon S3<br/>Static Website Files)]
      U -->|Open resume| CF
      CF -->|Serve content| S3
    end

    subgraph Counter["Visitor Counter"]
      JS[Website JavaScript]
      API[Amazon API Gateway<br/>HTTP API · GET /visitors]
      L[AWS Lambda<br/>Python]
      DB[(Amazon DynamoDB<br/>CloudNovaVisitors)]
      JS -->|GET /visitors| API
      API -->|Invoke| L
      L -->|Increment / read count| DB
      DB -->|Updated count| L
      L -->|JSON response| API
      API -->|Count| JS
    end

    CF -.->|Loads website containing| JS

    subgraph Deploy["CI/CD"]
      GH[GitHub Repository]
      GA[GitHub Actions]
      OIDC[AWS IAM OIDC Role]
      GH -->|Push to main| GA
      GA -->|Assume role| OIDC
      OIDC -->|Deploy website files| S3
    end
```

## Request flow

1. The visitor opens the website. CloudFront delivers the static files stored in S3.
2. The website JavaScript sends a request to API Gateway at `GET /visitors`.
3. API Gateway invokes the Python Lambda function.
4. Lambda increments the visitor count in DynamoDB and returns the updated count.
5. The website displays the returned count.
6. GitHub Actions deploys website changes to S3 using AWS IAM OIDC authentication.
