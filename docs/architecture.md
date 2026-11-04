# CloudNova — Architecture Diagram

```mermaid
flowchart LR
    V((Visitor)) -->|Opens site| CF[CloudFront]
    CF -->|Loads page| S3[(Amazon S3<br/>Website files)]

    S3 -.-> JS[Website JavaScript]
    JS -->|GET /visitors| API[API Gateway]
    API -->|Invokes| L[Lambda<br/>Python]
    L -->|Increment count| DB[(DynamoDB<br/>Visitor count)]
    DB -->|Updated count| L
    L -->|JSON response| API
    API -->|Displays count| JS

    GH([GitHub push]) --> GA[GitHub Actions]
    GA -->|OIDC| IAM[AWS IAM Role]
    IAM -->|Deploy files| S3

    classDef user fill:#EAF2FF,stroke:#2563EB,color:#12305A,stroke-width:2px;
    classDef web fill:#F0E9FF,stroke:#7C3AED,color:#3B176B,stroke-width:2px;
    classDef store fill:#E8F7EC,stroke:#239447,color:#124B27,stroke-width:2px;
    classDef api fill:#FFF0F5,stroke:#DB2777,color:#701A43,stroke-width:2px;
    classDef compute fill:#FFF3E0,stroke:#EA580C,color:#7C2D12,stroke-width:2px;
    classDef deploy fill:#E8F4FF,stroke:#0284C7,color:#0C4A6E,stroke-width:2px;

    class V user;
    class CF,JS web;
    class S3,DB store;
    class API api;
    class L compute;
    class GH,GA,IAM deploy;
```

## Flow

1. CloudFront serves the resume website files stored in S3.
2. Website JavaScript requests the visitor count from API Gateway.
3. API Gateway invokes Lambda, which increments the count in DynamoDB.
4. The updated count returns to the website and is displayed.
5. GitHub Actions deploys website changes to S3 using AWS IAM OIDC.
