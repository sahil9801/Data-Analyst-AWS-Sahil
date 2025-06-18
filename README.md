# Data-Analyst-AWS-Sahil

Cloud-Native Academic Data Platform: Architecture, Implementation, and Optimization on AWS


I. Introduction

This report details the comprehensive development and implementation of a cloud-native academic data platform leveraging Amazon Web Services (AWS). The initiative aims to migrate academic statistics processing and storage to the cloud, ensuring a scalable, secure, and efficient environment for managing critical datasets. The project encompasses foundational infrastructure deployment, advanced data ingestion and cleaning processes, and a strategic roadmap for future enhancements, all while adhering to cloud architecture best practices and cost optimization principles. This document serves as a comprehensive overview of the project's phases, technical methodologies, and the practical application of various AWS services, suitable for inclusion in a professional portfolio.

II. Project Overview: Academic Data Platform on AWS

The core objective of this project is to establish a robust cloud infrastructure for academic data, focusing on secure storage, efficient processing, and cost-effective operations. The platform's development has progressed through distinct phases, each building upon the previous to create a resilient and functional data ecosystem.

Phase 1: Foundational Infrastructure Deployment

The initial phase concentrated on establishing the core AWS infrastructure, including virtual servers for processing and a robust data repository. This foundational setup was crucial for providing a secure and scalable environment for academic data.
AWS EC2 Instance Deployment
A virtual server, identified by Instance ID i-0588c70d695df587a, was successfully launched in the US East (N. Virginia) region [Weekly Activity #2]. This region, us-east-1, was a deliberate choice due to its extensive service offerings, typically lower latency for North American users, and often competitive pricing, which is particularly beneficial for initial project phases where budget considerations are paramount. The instance type selected was t2.micro, chosen for its cost-effectiveness during initial testing and development, aligning with a budget-conscious project initiation [Weekly Activity #2]. This strategic selection allows for a lean start, with the flexibility to scale resources as project requirements evolve, demonstrating an agile and cost-aware approach to cloud resource provisioning.
The network configuration for the EC2 instance included the assignment of a public IPv4 address (3.238.108.10) for external accessibility and a private IP (172.31.8.8) for secure internal communication within the Virtual Private Cloud (VPC) [Weekly Activity #2]. This dual IP configuration represents a standard practice for managing access and maintaining internal network security.
AWS VPC Setup
A dedicated Virtual Private Cloud (VPC), named Academic-Vol-SahilSharma (VPC ID: vpc-0606z3b2cf24aef16), was configured with a CIDR block of 172.31.0.0/16 [Weekly Activity #2]. This configuration provides a large, isolated network space, which is critical for segmenting the academic data platform from other potential cloud resources. The dedicated VPC ensures network isolation, a fundamental security best practice that prevents unauthorized access and provides a controlled environment for sensitive academic data.
During the initial setup, challenges related to VPC configuration complexity arose, particularly concerning subnet and routing table configurations. These issues were effectively resolved by leveraging AWS’s default DHCP and route table settings, simplifying the setup process and demonstrating a pragmatic approach to problem-solving [Weekly Activity #2].
Security Group Configuration
A Security Group, Academic-SG-SahilSharma (ID: sg-0bf72259a5c832807), was created to manage inbound and outbound traffic for the EC2 instance [Weekly Activity #2]. This security group functions as a virtual firewall, restricting unauthorized access while permitting necessary protocols for data transfer. Initially, overly restrictive rules within the security group blocked SSH access. Adjustments were made to permit SSH (port 22) from trusted IP ranges, illustrating the need to balance stringent security measures with operational necessity to ensure administrative access [Weekly Activity #2]. The ability to identify and resolve these issues highlights practical experience in finding the appropriate balance between security and usability in cloud deployments.
AWS S3 Data Lake Foundation
A general-purpose S3 bucket, academic-raw-mah, was created in us-east-1 to serve as the primary storage for raw academic datasets [Weekly Activity #2]. S3 was chosen for its high durability, availability, scalability, and cost-effectiveness for object storage, making it an ideal initial landing zone for a data lake.
Security and Compliance Measures
To ensure robust security and compliance from the outset, IAM Access Analyzer was enabled for S3 [Weekly Activity #2]. This tool continuously monitors resource permissions, ensuring adherence to the principle of least privilege and proactively identifying any unintended public or cross-account access. Furthermore, AWS Storage Lens was activated to track storage usage trends and optimize costs for the S3 buckets [Weekly Activity #2]. This provides granular visibility into storage metrics, enabling informed decisions on data lifecycle management and cost reduction. The immediate activation of these governance tools indicates a strong emphasis on proactive security and cost optimization, reflecting a mature understanding of cloud operations and best practices.
Project Documentation & Collaboration
A structured directory (Group 8 - Academic > Week #2 > Academic Data Team > Design) was established on AWS to facilitate team collaboration and organized resource management [Weekly Activity #2]. The "Academic Data Lake Design" document was uploaded and updated, outlining the architecture for data ingestion and processing, which ensures architectural consistency and serves as a central reference [Weekly Activity #2]. Supplementary diagrams, including fishbone and Draw.io, were created to visualize workflows and dependencies, promoting alignment across stakeholders [Weekly Activity #2].
The following table summarizes the foundational AWS infrastructure deployed in Phase 1:
Table 1: Phase 1 AWS Infrastructure Overview

AWS Service
Resource Name/ID
Key Configuration/Specifications
Purpose/Benefit
EC2
i-0588c70d695df587a
t2.micro, us-east-1, Public IP: 3.238.108.10
Virtual Server for Processing
VPC
Academic-Vol-SahilSharma (vpc-0606z3b2cf24aef16)
CIDR: 172.31.0.0/16
Network Isolation
Security Group
Academic-SG-SahilSharma (sg-0bf72259a5c832807)
SSH (Port 22) from trusted IPs
Inbound/Outbound Traffic Control
S3 Bucket
academic-raw-mah
us-east-1, General-purpose
Raw Data Storage
IAM Access Analyzer
Enabled for S3
Monitors S3 permissions
Security Compliance
AWS Storage Lens
Activated
Tracks storage usage/costs
Cost Optimization


Phase 2: Data Ingestion, Cost Optimization & Cleaning

Building upon the established infrastructure, Phase 2 focused on optimizing data storage costs and implementing serverless data cleaning processes.
AWS S3 Cost Analysis
A detailed cost estimation for S3 data storage was performed, revealing a highly cost-effective ingestion pipeline [Weekly Activity #3]. The upfront cost was $4.37 USD (one-time), with a projected monthly cost of $0.02 USD, leading to a 12-month total of $4.61 USD [Weekly Activity #3]. These minimal costs are primarily attributed to the serverless architecture employed and optimized S3 storage. The storage details indicate a volume of 1 GB/month of S3 Standard Storage, with an average object size of 1.2 KB and low request volume [Weekly Activity #3]. This demonstrates a direct link between adopting serverless technologies and achieving significant cost savings, particularly for variable or low-volume data processing workloads, as serverless models eliminate idle resource costs and scale automatically.
AWS Glue DataBrew Implementation
AWS Glue DataBrew was implemented for serverless data cleaning and profiling [Weekly Activity #3]. The service analyzed key dataset columns, including CompletionID, StudentID, CourseID, and CompletionStatus [Weekly Activity #3]. A significant outcome was the achievement of 100% data validity across all analyzed columns, indicating successful data cleansing and adherence to defined quality standards [Weekly Activity #3]. This validation of dataset integrity is a critical prerequisite for any reliable downstream analytics, as it prevents the propagation of inaccuracies. DataBrew also facilitated the identification of distinct and unique values for trend analysis, such as course completion rates, showcasing its capability for preliminary data exploration and insight generation [Weekly Activity #3]. The successful validation of dataset integrity establishes a reliable source for subsequent reporting and machine learning initiatives.
S3 Data Organization & Pipeline Execution
A new S3 bucket, academic-cln-sahil, was created to store the cleaned data [Weekly Activity #3]. This bucket is strategically organized with partitioned folders, including Course Completion Records, Student Demographics, Graduation Applications, and Retention Records [Weekly Activity #3]. CSV outputs from profiling and cleaning jobs, such as Profiling-Job-Results.csv, are stored within these partitions, ensuring interoperability with various analytics tools [Weekly Activity #3]. Automation was achieved by partitioning data by attributes like StudentID and CreditsEarned for efficient querying [Weekly Activity #3]. This partitioning strategy is crucial for enhancing performance and optimizing costs in data lakes, particularly when utilizing services like AWS Athena, as it significantly reduces the amount of data scanned during queries.
The following table summarizes the key metrics and activities from Phase 2:
Table 2: Phase 2 Data Processing & Cost Metrics

Metric/Activity
Details/Outcome
Significance
S3 Monthly Cost
$0.02 USD
Demonstrates cost-effectiveness of serverless storage.
S3 Storage Volume
1 GB/month
Baseline for initial data volume.
DataBrew Data Quality
100% Validity
Ensures reliability for downstream analytics.
Cleaned S3 Bucket
academic-cln-sahil
Structured repository for processed data.
Data Partitioning
By StudentID, CreditsEarned
Optimizes query performance and cost for analytics.


Strategic Roadmap and Future Enhancements

The project's ongoing development includes several critical next steps aimed at further optimizing the platform and expanding its capabilities.
Data Migration: The immediate next step involves beginning the transfer of academic datasets to the academic-raw-mah bucket using AWS CLI/SDKs [Weekly Activity #2]. This is the logical progression from infrastructure setup to populating the data lake.
Automation (S3 Lifecycle): Implementation of lifecycle policies in S3 is planned to automatically archive older, infrequently accessed data to Glacier, which will significantly reduce storage costs over the long term [Weekly Activity #2]. This demonstrates a crucial strategy for long-term cost management.
EC2 Scaling: Continuous monitoring of the EC2 instance performance is planned, with a provision to upgrade to a larger instance type if CPU/memory usage consistently exceeds predefined thresholds [Weekly Activity #2]. This highlights the elasticity of cloud computing and the importance of performance monitoring to ensure optimal resource allocation.
Access Controls (IAM): Finalizing IAM roles and bucket policies is a priority to grant granular access to team members [Weekly Activity #2]. This reinforces the commitment to the principle of least privilege and ensures secure collaboration within the project.
Expand DataBrew Jobs: The application of additional transformations, such as handling missing values, for other datasets is planned [Weekly Activity #3]. This indicates a continuous improvement approach to data quality and pipeline robustness.
Integration with Analytics Tools: A key objective is to connect the cleaned S3 data to analytics tools such as AWS Athena and Amazon QuickSight [Weekly Activity #3]. This is the ultimate goal of the data platform: enabling efficient data consumption and insight generation for academic stakeholders.
Stakeholder Review: Sharing cleaned datasets with academic teams for validation is an important step to ensure data accuracy and user satisfaction [Weekly Activity #3]. This emphasizes the collaborative nature of the project and the importance of data governance with end-users.
The extensive nature of these "Next Steps" underscores that cloud projects are inherently iterative and evolutionary, rarely a "set and forget" endeavor. They require continuous monitoring, optimization, and expansion based on evolving needs and data growth, reflecting a fundamental understanding of DevOps principles and the dynamic nature of cloud environments. Furthermore, the explicit mention of connecting cleaned S3 data to analytics tools reveals the broader strategic intent behind building this data platform. The EC2/S3/Glue DataBrew setup is not an end in itself; it serves as the foundational layer for enabling advanced data analytics, reporting, and potentially machine learning initiatives, thereby unlocking greater value from the academic data.

III. Foundational AWS Services: Case Studies and Practical Applications

The project's success is underpinned by a practical understanding and application of several core AWS services, each contributing to the platform's robustness, security, and efficiency. The following sections detail the relevance of these services, drawing upon both project implementation details and insights from associated case studies and labs.

AWS Deployment and Service Models (Module 1)

This section delves into the fundamental concepts of cloud computing, specifically focusing on AWS's interpretation of deployment models (Public, Private, Hybrid) and service models (Infrastructure as a Service - IaaS, Platform as a Service - PaaS, Software as a Service - SaaS). The project primarily leverages IaaS for foundational compute (EC2) and networking (VPC), while utilizing PaaS/Serverless services (S3, Glue DataBrew) for data storage and processing. This hybrid service model approach optimizes for control where granular management is required (e.g., specific EC2 configurations) and leverages managed services for efficiency and scalability where possible (e.g., S3's inherent scalability, DataBrew's serverless operations) [Image 10].
The project's architecture demonstrates a strategic blending of cloud service models for optimal resource utilization. EC2, as an IaaS offering, provides granular control over the compute environment, which may be necessary for specific academic applications or potential integration with legacy software. Conversely, S3 and Glue DataBrew, aligning more closely with PaaS/Serverless models, abstract away underlying infrastructure management, thereby reducing operational overhead and offering inherent scalability and cost-efficiency, as evidenced by the low S3 costs achieved. A well-designed cloud architecture often involves a thoughtful blend of service models to achieve the right balance of control, cost, scalability, and operational simplicity for different components of the solution.
Table 3: Cloud Deployment Models Comparison

Deployment Model
Characteristics
Key Benefits
Relevance to Academic Platform
Public Cloud
Owned & operated by a third-party cloud provider; shared resources.
High scalability, cost-effectiveness, minimal management.
Core services (EC2, S3, DataBrew) deployed on AWS public cloud.
Private Cloud
Dedicated to a single organization; can be on-premise or hosted.
Greater control, enhanced security, compliance.
Potential for hybrid integration with on-premise academic systems for sensitive data or legacy applications.
Hybrid Cloud
Combines public and private clouds, allowing data/apps to move between them.
Flexibility, optimized resource utilization, compliance.
Current architecture leans public; future integration with on-premise data sources would create a hybrid model.


AWS Cost Analysis and Optimization (Module 2)

This section elaborates on AWS's pay-as-you-go pricing model, the factors influencing costs (compute, storage, data transfer, requests), and key cost management strategies such as rightsizing, reserved instances, spot instances, and leveraging managed services. The project's S3 cost analysis, revealing minimal monthly expenditures, directly illustrates the economic benefits of serverless architecture and optimized storage. The use of the AWS Pricing Calculator for upfront cost estimation and the understanding of AWS Support Plans are integral to managing operational costs [Image 9].
Proactive cost management is a core cloud skill, not merely an afterthought. The explicit S3 cost analysis in Weekly Activity #3, combined with the module's focus on the AWS Pricing Calculator and Support Plans, underscores that cost management is an integral part of cloud architecture. The low S3 costs achieved are a direct result of optimized storage and serverless choices. This demonstrates that a cloud architect must possess not only technical deployment skills but also a strong understanding of cloud economics and the tools available to manage and optimize spending. This proactive approach to cost analysis is crucial for long-term project viability and stakeholder confidence.
Table 4: Project AWS Cost Breakdown and Optimization Strategies

Cost Category
Actual/Estimated Cost
Optimization Strategy Applied/Considered
Impact/Benefit
S3 Storage
$0.02/month
Serverless architecture, Lifecycle policies (Glacier)
Minimal storage cost, long-term savings.
EC2 Compute
Implicitly low (t2.micro)
Rightsizing, Monitoring for scaling
Cost-effective for initial testing, performance optimization.
Data Transfer
Minimal (initial phase)
Future use of VPC endpoints, CloudFront for egress
Reduced data transfer costs for high volume.
AWS Glue DataBrew
Pay-per-use (serverless)
Optimized job execution, efficient data partitioning
Cost-efficient data processing for variable workloads.


AWS Global Infrastructure (Module 3)

This section explains the hierarchical structure of AWS Global Infrastructure: Regions (geographical areas), Availability Zones (isolated locations within a region), and Edge Locations (for content delivery). The project's deployment in us-east-1 leverages the benefits of a robust region, ensuring high availability and fault tolerance by implicitly distributing resources across multiple Availability Zones [Weekly Activity #2]. Edge locations would be relevant for future content delivery network (CDN) integration (e.g., CloudFront) for academic portals [Image 8].
Deploying in us-east-1 is a strategic decision that leverages regional design for inherent resilience and scalability. AWS's global infrastructure, particularly the concept of Regions and Availability Zones (AZs), is designed for high availability and fault tolerance. By deploying in a region, the project inherently benefits from the redundancy provided by multiple, isolated AZs. This means that even if one AZ experiences an outage, services can remain operational in another AZ within the same region. Choosing a robust region like us-east-1 and understanding its underlying AZ structure is a foundational architectural decision that directly contributes to the platform's resilience and scalability, minimizing potential downtime for academic data access and processing.
Table 5: AWS Global Infrastructure Components & Project Relevance

Component
Description
Role in High Availability/Performance
Project Relevance
Region
A geographical area with multiple isolated locations (Availability Zones).
Provides isolation and fault tolerance across large geographies.
us-east-1 chosen for primary deployment due to feature richness and cost.
Availability Zone
One or more discrete data centers with redundant power, networking, and connectivity within a Region.
Ensures high availability and fault tolerance within a region; services can failover between AZs.
Resources implicitly distributed across AZs within us-east-1 for resilience.
Edge Location
Data centers owned by AWS that deliver content to end-users with low latency.
Improves content delivery performance for global users (e.g., CloudFront).
Relevant for future CDN integration for academic portals or public-facing applications.


AWS Identity and Access Management (IAM) (Module 4)

This section covers IAM users, groups, roles, and policies, explaining how IAM is fundamental for securely controlling access to AWS resources. The project utilized IAM Access Analyzer for S3, demonstrating a commitment to monitoring resource permissions and enforcing the principle of least privilege [Weekly Activity #2]. This ensures that only authorized entities (users, roles) have the necessary permissions to interact with the academic data [Image 6, Image 7].
IAM serves as the bedrock of cloud security and compliance. The explicit enabling of "IAM Access Analyzer for S3" to "monitor resource permissions and ensure compliance with least-privilege principles" is a critical security practice. IAM is the primary mechanism for controlling who can do what in AWS. The use of Access Analyzer shows a proactive stance on security, continuously verifying that permissions are not overly permissive. Robust IAM implementation, guided by the principle of least privilege, is paramount for preventing unauthorized access, data breaches, and maintaining compliance. Without strong IAM, even well-configured services can be vulnerable.
Table 6: Key IAM Best Practices & Project Application

IAM Best Practice
Description
Project Application/Benefit
Principle of Least Privilege
Grant only the minimum permissions necessary for a task.
IAM Access Analyzer for S3, granular access for team members (Next Steps)
Use IAM Roles
Assign temporary credentials to services and EC2 instances.
Implicit for EC2/S3 interaction; secure service-to-service communication.
Enable MFA for Users
Require multi-factor authentication for console access.
(Implicitly recommended as a general best practice)
Regular Audits
Periodically review IAM policies and access logs.
IAM Access Analyzer provides continuous monitoring.


AWS Virtual Private Cloud (VPC) (Module 5)

This section describes how AWS VPC allows users to provision a logically isolated section of the AWS Cloud where they can launch AWS resources in a virtual network that they define. Key components include CIDR blocks, subnets (public/private), route tables, internet gateways, and NAT gateways. The project's dedicated VPC (Academic-Vol-SahilSharma with CIDR 172.31.0.0/16) is a direct application of VPC concepts, ensuring network isolation for the academic data platform [Weekly Activity #2]. The challenges faced with initial VPC configuration and security group rules, and their successful mitigation, provide real-world insights into effective VPC management [Image 4, Image 5].
The VPC serves as the foundation for network security and segmentation. The project's use of a dedicated VPC is a fundamental security and architectural decision. VPCs provide network isolation, meaning the academic data platform's resources are logically separated from other AWS customers' resources and even other projects within the same AWS account. This granular control over the network environment is critical for defining secure communication paths, implementing virtual firewalls (Security Groups), and ensuring data privacy. A well-designed VPC is the cornerstone of network security in AWS, enabling robust segmentation and controlled access, which is paramount for sensitive academic data.
Table 7: Project VPC Configuration Details

Component
Configuration/Value
Purpose/Role
VPC ID
vpc-0606z3b2cf24aef16
Logical network isolation for academic data platform.
CIDR Block
172.31.0.0/16
Defines the private IP address range for the VPC.
Public IP
3.238.108.10
External access point for the EC2 instance.
Private IP
172.31.8.8
Internal communication within the VPC for EC2.
Security Group
Academic-SG-SahilSharma
Controls inbound/outbound traffic for the EC2 instance.
Region
US East (N. Virginia)
Geographic location of the VPC and resources.


AWS Lambda for Serverless Computing (Module 6)

This section introduces AWS Lambda as a serverless compute service that runs code in response to events and automatically manages the underlying compute resources. It covers event-driven architecture, scalability, and cost efficiency. While not explicitly used in the initial weekly reports, Lambda is a natural fit for future automation within the academic data pipeline. Potential applications include triggering data processing jobs upon S3 object creation, executing small ETL tasks, or responding to data quality alerts [Image 3].
Lambda is a powerful enabler of event-driven automation and cost-optimized microservices. Its serverless, event-driven nature means it only runs when triggered, leading to significant cost savings compared to always-on servers. It is ideal for tasks like triggering data processing when new files land in S3 or for small, specific transformations. Lambda is a powerful tool for building highly scalable, cost-efficient, and decoupled microservices within a data pipeline, moving towards a more modern, event-driven architecture. Its potential integration (e.g., triggering DataBrew jobs, sending notifications) represents a natural evolution of the platform's automation capabilities.
Table 8: Potential AWS Lambda Use Cases for Academic Data Platform

Use Case
Description
Benefit
S3 Event Trigger
Automatically trigger data processing when new files are uploaded to S3.
Real-time data ingestion, reduced manual effort, immediate processing.
Data Validation
Run quick, lightweight data quality checks on incoming records.
Early detection of data issues, ensuring data integrity upstream.
Notification Service
Send alerts for pipeline failures, data anomalies, or completion.
Improved operational awareness, proactive issue resolution.
ETL Microservices
Execute small, specific data transformations or aggregations.
Decoupled architecture, highly scalable, cost-efficient for bursty workloads.


AWS Elastic Block Store (EBS) for Persistent Storage (Module 7)

This section describes AWS EBS as block-level storage volumes for use with EC2 instances. It covers different volume types (e.g., General Purpose SSD, Provisioned IOPS SSD, Throughput Optimized HDD, Cold HDD) and their performance characteristics, use cases, and data durability features (snapshots). EBS volumes are implicitly attached to the EC2 instance launched in Week 2, providing persistent storage for the operating system, applications, and any temporary data processed directly on the server. This ensures data remains even if the instance is stopped or terminated (if configured correctly) [Image 2].
EBS serves as the backbone for statefulness and performance-critical workloads on EC2. While S3 is utilized for the data lake, EBS is implicitly critical for the EC2 instance. EBS provides persistent, high-performance block storage, which is essential for the operating system, application binaries, and any databases or temporary files that reside directly on the EC2 server. Unlike ephemeral instance storage, EBS volumes can be detached and reattached, ensuring data durability independent of the EC2 instance's lifecycle. EBS is crucial for maintaining stateful applications and providing the necessary I/O performance for compute-intensive tasks on EC2, forming a complementary storage solution to S3 within the overall architecture. This highlights the distinction between object storage (S3) and block storage (EBS) and their respective optimal use cases.
Table 9: AWS EBS Volume Types and Use Cases

EBS Volume Type
Description
Recommended Use Case
Relevance to Project EC2
General Purpose SSD (gp2/gp3)
Balanced price/performance for a wide variety of workloads.
Boot volumes, dev/test environments, small to medium databases.
Likely used for the EC2 OS and application files, balancing cost and performance.
Provisioned IOPS SSD (io1/io2)
Highest performance SSD volumes for critical applications.
Large relational/NoSQL databases, high-transaction workloads.
Potential for future EC2 scaling if compute-intensive tasks demand higher I/O performance.
Throughput Optimized HDD (st1)
Low-cost HDD for frequently accessed, throughput-intensive workloads.
Big data, data warehouses, log processing.
Less relevant for current EC2 use, but useful for large sequential workloads.
Cold HDD (sc1)
Lowest cost HDD for infrequently accessed data.
Colder data, large sequential data access.
Not directly applicable to EC2 boot/app volume, but useful for archival if attached.


IV. Conclusion and Portfolio Reflection

The project has successfully established a robust, scalable, and secure cloud-native academic data platform on AWS. Through the foundational deployment of EC2 and S3, the implementation of cost-efficient data ingestion and cleaning with Glue DataBrew, and the adherence to best practices in security and cost management, the platform is well-positioned for future data processing and analytics initiatives.
Key learnings from this project include invaluable hands-on experience in cloud infrastructure deployment, network configuration, security hardening, and serverless data processing. The iterative nature of cloud development was reinforced, emphasizing the importance of continuous monitoring, optimization, and adaptation in a dynamic cloud environment. Challenges encountered, such as VPC configuration complexities and security group rule adjustments, provided practical lessons in troubleshooting and balancing operational needs with stringent security requirements.
This project serves as a comprehensive portfolio piece, demonstrating proficiency across a wide array of core AWS services. It showcases the practical application of cloud architecture principles, problem-solving capabilities, and a commitment to building secure, scalable, and cost-effective solutions. The detailed documentation, including architectural choices, challenges overcome, and a clear roadmap for future enhancements, highlights a strong understanding of the entire project lifecycle. This experience is highly relevant for potential employers or academic assessment in cloud computing and data engineering roles.
