# 🛒 Scalable E-commerce Platform on AWS (Order Management Focus)

## 📌 Introduction
This project implements a **scalable, fault-tolerant, and high-performance e-commerce platform** using AWS services. The architecture ensures seamless **order management** while optimizing costs, security, and availability.

---

## 🏗️ **Key Components**
- **Web Tier**: Amazon EC2 instances behind an Application Load Balancer (ALB)
- **Database Layer**: Amazon RDS with Multi-AZ for high availability
- **Storage & Content Delivery**: Amazon S3 & Amazon CloudFront
- **Scalability**: Auto Scaling Groups for handling traffic fluctuations
- **Order Processing**: AWS Lambda, API Gateway, Amazon SQS, and Amazon DynamoDB
- **Security**: AWS IAM, Security Groups, and VPC configurations
- **DevOps & CI/CD**: AWS CodePipeline, CodeBuild, and CodeDeploy
- **Monitoring & Logging**: Amazon CloudWatch & AWS X-Ray
- **Disaster Recovery**: AWS Backup and replication strategies

---

## 🚀 **AWS Services Involved**
| Service        | Purpose |
|---------------|---------|
| EC2 + ALB | Web hosting with load balancing |
| RDS (Multi-AZ) | Relational Database for order & user data |
| DynamoDB | NoSQL database for real-time order tracking |
| S3 + CloudFront | Static content hosting & caching |
| API Gateway | Manages API requests for order processing |
| Lambda | Serverless functions for order validation |
| SQS | Message queuing for async order processing |
| SNS | Notification service for order status updates |
| IAM + Security Groups | Access control & security |
| CodePipeline | Automates deployment pipeline |
| CloudWatch | Performance monitoring & logging |

---

## 🔄 **Workflow Highlights (Order Management)**
1. **User places an order** → Request hits **ALB → EC2 → API Gateway**.
2. **API Gateway** triggers an **AWS Lambda** function for order validation.
3. **Lambda** checks **inventory in DynamoDB**.
4. **Order request** is placed into an **SQS queue** for async processing.
5. **Order Processor (Lambda/EC2 worker)** picks orders from **SQS** and updates **RDS**.
6. **SNS triggers notifications** (Email/SMS) to users about order status.
7. **CloudWatch logs & metrics** track order processing performance.

---

## 📊 **Architecture Diagram**
```mermaid
graph TD;
    User -->|Places Order| ALB;
    ALB -->|Routes Traffic| EC2;
    EC2 -->|API Request| APIGW;
    APIGW -->|Order Validation| Lambda;
    Lambda -->|Check Stock| DynamoDB;
    Lambda -->|Enqueue Order| SQS;
    SQS -->|Order Processing| Worker[EC2 Worker/Lambda];
    Worker -->|Update Order Status| RDS;
    Worker -->|Send Notification| SNS;
    SNS -->|Notify User| Email/SMS;
    CloudWatch -->|Logs & Monitoring| Admin;
