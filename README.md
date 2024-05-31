# Module 4 - Solution Architecting (National Day Parade)
### Main Requirements / Goals
1. Techstack
    - ReactJS (Frontend)
    - Node.js (Backend)
    - PostgreSQL (Database)
2. Important Requirements
    - Deployed swiftly
    - Application Security
    - Highly Available (and durable)
    - Meets 6 Pillars of the Well-Architected Framework (Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainabililty)
3. Inference (From current NDP web application)
    - Mainly serving static content (Images, Libraries, CDN, PDFs, Infographics, etc)
    - Embeded content (YouTube Video - external)
    - Ticketing Application (via SingPass/form.gov.sg - external)
    - Overall, light application as most heavy assets/logic are done externally

## Answer

### Architecture Diagram
[![Architecture Diagram][architecture-diagram]](https://github.com/Vasn/SES-Cloud-Homework3)

### Other notable services to be used (not in diagram)
- Elastic Beanstalk - managed service for backend deployment which handles autoscaling, load balancing, monitoring and launching instances
- Terraform/CloudFormation - IaC tool to automate, store and manage infrastructure resources/configuration.
- CloudWatch/X-Ray - application/infrastructure/request monitoring and alerting system
- IAM - identity access management, manage users, services, resources, roles & permissions
- Key Management Service - for encryption of data/signing
- Secrets Manager - for storing secrets (e.g. database/API keys)

### Explanation of Well-Architected Framework
1. Operational Excellence
    - Managed Service: Resources like S3 instead of EC2 for static web hosting and asset storage would be more effective in the long term as managed services like S3, RDS, Elastic Beanstalk, etc reduces operational burden where possible, allowing users to focus on their core business problem.
    - Infrastucture/Operations as Code: Allows us to write, store, version, update our resources with code, limiting human errors, increasing reusability and automating resource provisionining.
    - Observability: Services like CloudWatch and X-Ray let us to define and monitor metrics that represents information like your KPIs, allowing us to monitor and regularly review and update our KPIs.

2. Security
    - Confidentiality: Processes like encryption with KMS maintains confidentiality and prevents unauthorised access.
    - (Data) Integrity: Enforcing access control (IAM) and encryption allows protection of data in transit and rest as well as prevention of data tampering.
    - Availability: With services like WAF, Shield, CloudFront and ALB, they act as a layer of protection again attacks like DDoS which takes away availability of the service/data.
    - Managing user/roles/permissions: Tools like IAM is able to centralise identity management and remove long term static credentials. Following principle of least privilege and enforcing separation of duties are essential in this step.
    - Security Controls (Prevention/Detection/Alerting): Controls set with tools like CloudWatch, security groups and network controls (like VPC/subnets) helps in crerating an environment where there is tracability, security at all layers and preparation for security events.
3. Reliability
    - Resiliency/Reliability: Health Checks done in services like Auto Scaling groups and Route 53 ensures that endpoints or instances are healthy, else automatic failover or reprovisioning of instances will happen.
    - Availability/Disaster Recovery: Deployment methods like Multi-AZ/Primary-Standby/Blue-Green deployment ensures high availability and the option for automatic failover, increasing uptime.
4. Performance Efficiency
    - Using computing resources efficiently: Utilising resources like S3 and CloudFront can enhance scalability and low latency, while maintaining cost effectiveness for serving static frontend assets.
    - Maintain performance/efficiency overtime: In-memory ram caching services like elasticache allows for a quicker response time by caching, while reducing read loads on the primary database instance.
5. Cost Optimization
    - Practice Cloud Financial Management/Expenditure and usage awareness: Able to measure, optimise, plan, forecast financially with tools like AWS Cost Explorer, Usage Reports, AWS Organizations, etc.
    - Manage demand and supply resources: With processes like autoscaling groups, you can remove excess unused resources when service demand drrops to prevent overspending.
    - Optimize over time/Cost effective resources: Based on monitioring and forecasting resource usage level, you can determine base usage (e.g. for EC2 instance and purchase spot instances, instead of on-demand instances)
6. Sustainabililty
    - Optimized Resource Utilisation: With processes like autoscaling groups, load balancers and CDNs, we ensure that resources are not over provisioned and under untilised. This allows us to continue to meet demarrd while aligning our service levels to our customerr needs
    - Monitoring: To ensure sustainability, constant improvements is required through setting sustainability goals > monitoring > forecasting > adapting/anticipating. This allows us to continuously evaluate and use more efficient hardware, software and processes.

### Other notable comparisons/considerations
1. Frontend S3 vs EC2
2. Backend EC2 vs Containerisation
3. Elasticache vs Read-replica instances

## Resources Referenced
- https://aws.amazon.com/architecture/well-architected/
- https://docs.aws.amazon.com/
- https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts-webserver.html?icmpid=docs_elasticbeanstalk_console
- https://d1.awsstatic.com/architecture-diagrams/ArchitectureDiagrams/web-application-architecture-on-aws-ra.pdf?did=wp_card&trk=wp_card

[architecture-diagram]: assets/Module-4-Architecture.jpg