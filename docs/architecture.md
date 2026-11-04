# CloudNova — Architecture

A clean overview of the deployed resume website, visitor counter, and automated deployment.

```mermaid
flowchart TB
    Visitor([Visitor / Browser])

    subgraph WEB["1 · Resume Website"]
      direction LR
      CF["Amazon CloudFront<br/>CDN"] -->|"Fetches site files"| S3[("Amazon S3<br/>Static website files")]
    end

    subgraph COUNT["2 · Visitor Counter"]
      direction LR
      FE["Website JavaScript"] -->|"GET /visitors"| API["Amazon API Gateway<br/>HTTP API"]
      API -->|"Invoke"| Lambda["AWS Lambda<br/>Python"]
      Lambda -->|"Increment count"| DB[("Amazon DynamoDB<br/>CloudNovaVisitors")]
      DB -->|"Updated count"| Lambda
      Lambda -->|"JSON response"| API
      API -->|"Visitor count"| FE
    end

    Visitor -->|"Opens website"| CF
    CF -->|"Delivers page"| Visitor
    S3 -.->|"Website includes"| FE

    subgraph CICD["3 · Automated Deployment"]
      direction LR
      GitHub["GitHub Repository"] -->|"Push to main"| Actions["GitHub Actions"]
      Actions -->|"OIDC role assumption"| IAM["AWS IAM Role"]
      IAM -->|"Deploy static files"| S3
    end

    classDef visitor fill:#EAF2FF,stroke:#2563EB,color:#12305A,stroke-width:1.5px;
    classDef edge fill:#F0E9FF,stroke:#7C3AED,color:#3B176B,stroke-width:1.5px;
    classDef storage fill:#E8F7EC,stroke:#239447,color:#124B27,stroke-width:1.5px;
    classDef api fill:#FFF0F5,stroke:#DB2777,color:#701A43,stroke-width:1.5px;
    classDef compute fill:#FFF3E0,stroke:#EA580C,color:#7C2D12,stroke-width:1.5px;
    classDef deploy fill:#E8F4FF,stroke:#0284C7,color:#0C4A6E,stroke-width:1.5px;

    class Visitor visitor;
    class CF edge;
    class S3,DB storage;
    class API api;
    class Lambda compute;
    class FE,GitHub,Actions,IAM deploy;

    style WEB fill:#F8FAFF,stroke:#93B4E8,stroke-width:1.5px
    style COUNT fill:#FFFAFC,stroke:#E9A3C4,stroke-width:1.5px
    style CICD fill:#F4FAFF,stroke:#7CC4E8,stroke-width:1.5px
```

## How it works

1. A visitor opens the resume website. CloudFront delivers the static files stored in S3.
2. The website JavaScript calls API Gateway at `GET /visitors`.
3. API Gateway invokes the Python Lambda function.
4. Lambda increments the visitor count stored in DynamoDB.
5. The updated count returns through API Gateway and appears on the website.
6. GitHub Actions deploys website updates to S3 using AWS IAM OIDC—no long-lived AWS keys are stored in GitHub.
