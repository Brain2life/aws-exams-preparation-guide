# Mini notes and tips

These short notes and tips will help you to eliminate the wrong options and choose the correct answer(s).

## Table of contents
- [AWS Solutions Architect Pro](#aws-solutions-architect-pro)
    - [Migrations](#migrations)
    - [Desing a new solution](#desing-a-new-solution)
    - [Improvement for existing solutions](#improvement-for-existing-solutions)

## AWS Solutions Architect Pro

### Migrations and Modernizations

- If you want to migrate applications and workloads from on-premises to the cloud in **cost-effective** way, then use - **[AWS Application Migration Service](https://tutorialsdojo.com/aws-application-migration-service/)**. It uses **lift and shift** strategy.
- If you want to migrate workloads from on-premises to the cloud in a **faster way**, use **[AWS Direct Connect Service](https://tutorialsdojo.com/aws-direct-connect/)**. However, it can be **costly**. It uses **private network of AWS** to transfer data. 
- Use **[AWS VM Import/Export](https://aws.amazon.com/ec2/vm-import/)** service for **cost-effective** migration of servers from on-premises to the cloud. As this service, do not charge for import/export operation, beyond standard charges for EC2 and S3 services. 
- If you need to **enable security patch-management for an Oracle RAC cluster during migration from on-premises to AWS and backup in a least efforts manner**, use **automated EBS snapshot creation for EC2 by using Amazon Data Lifecycle Manager and use  AWS Systems Manager Patch Manager for patching**. **AWS RDS and Aurorora does not support Oracle RAC clusters**.
- If you need to **migrate on-premises database on EC2 instances backed by EBS volumes following the most cost-effective and throughput oriented solution**, use **AWS Database Migrations service and Cold HDD sc1 EBS volumes for cost savings**.
- If you want to have the **cheapest and archival storage solution, use S3 Glacier**.
- Transfering **data from on-premises to S3 bucket via Snowball Edge device** can be **slow due to encryption overhead**. To **improve performance open multiple parallel copy jobs**.
- If you need to **migrate workloads from on-premises to AWS managed services like AWS RDS and Elastic Beanstalk and in cost-effective way**, then use **replatform strategy**. For more information, see the following diagram:
- If you need to **provide a self-service portal without complex details to your developers, data scientists, use AWS Service Catalog with SageMaker**.

![](../img/sap_migration_paths.png)

### Desing a new solution
- If you need a service to **orchestrate** your workloads and that is **serverless**, use [**Step Functions**](https://tutorialsdojo.com/aws-step-functions/) with **Lambda**. This allows to **minimize the operational overhead**.
- If you need to **limit outbound web connections from your VPC to the internet** and **filter requests based on URLs**, then **use a forward web proxy** with custom domain whitelists or DNS content filtering services. For more information, see [How to set up an outbound VPC proxy with domain whitelisting and content filtering](https://aws.amazon.com/blogs/security/how-to-set-up-an-outbound-vpc-proxy-with-domain-whitelisting-and-content-filtering/)
- If you need to achieve **better availability and bandwidth with minimal efforts** to setup **Internet connection**, use **NAT Gateways** instead of NAT Devices. For more information, see [Compare NAT gateways and NAT instances](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html)
- If you need a **scalable solution** that can **handle a sudden spikes in traffic** use **CloudFront**, **Elstic Load Balancer**, **SQS** and **AutoScaling**. 
- If you need to implement **limit access to resources in different accounts** and implement **resource-based permissions** in **multi-account environment**, use **AWS Organizations with IAM roles with identity and resource based policies**. SCPs are not sufficient, they act as a guardrail on OU level. You have to use IAM roles. For more information, see [IAM tutorial: Delegate access across AWS accounts using IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_cross-account-with-roles.html)
- If you need to implement **data processing solution** with **high network performance**, **scalable** and **near-realtime**, then consider to use **AWS Direct Connect** for network part, **auto-scaling groups** for scalability, **Amazon Kinesis Data Streams** for data consumption and processing and **API Gateway Websocket API** for real-time applications such as chat applications, collaboration platforms, multiplayer games, and financial trading platforms. For more information about WebSockets, see [WebSockets in 100 Seconds & Beyond with Socket.io](https://www.youtube.com/watch?v=1BfCnjr_Vjg)
- If company is using an existing **Microsoft Active Directory on-premises** and it needs to **extend it to AWS** and enable **SSO**, then use **AWS Directory Service for Microsoft AD** to create secure Windows trusts between your on-premises Microsoft Active Directory domains and your AWS Microsoft AD domain in the AWS Cloud. 
- If you need to **serve private content for a particular group of users in specific geographic location**, you can use **CloudFront signed URLs or signed cookies** with **S3 pre-signed URLs** and **disable access to S3 by using direct URLs**.
- If you need to **implement cost-effective and efficient search feature**, then **use S3 for data storage, Amazon OpenSearch Service for query processing and use Elastic Beanstalk for app deployments**.
- If you need **strong server side encryption in S3 with multi-factor encryption**, then use **Amazon S3-managed encryption keys (SSE-S3)**.
- If you need to **transcribe (convert speech to text) voice call recordings**, use **Amazon Transcribe**. If you need to **move data to long term storage after 90 days, configure S3 lifecycle policy to move data to S3 Glacier**.
- If you need to **collect sensor data, use AWS IoT Core Basic Ingest**. **To enrich data and avoid operational overhead**, use **AWS Data Firehose with Lambda**.
- If you need **DDoS protection, control your traffic and secure your applications from common web exploits (SQL injection, JS XSS, etc) use AWS Shield and AWS WAF**.
- If you **enable versioning on S3 bucket with files in there, these files will have an initial version `null`**. Then **with each update of files the versioning of files will change as well**.
- If you need to **enable HTTPS for public website, use public certificate in ACM. Public ACM certificate can be used on Load Balancers. Private ACM certificates are used only on EC2 instances**. **Public ACM is free, while private ACM is charged on monthly basis**. 
- If you need to **provide access to resources for a third-party AWS account, third-party account should create an External ID that will be given to the source account**. **Create an IAM role with the required access and put the External ID in the IAM role’s trust policy**.
- If you need to **create a stateless and REST compliant service**, use **AWS API Gateway with Lambda proxy integration**. To **authenticate and securely process all requests**, use **AWS Cognito User Pools**.
- If you want a **highly available solution in one region and with configured passive backup of running application in another region**, then use **EC2 Auto-Scaling Group** and **Route53 with failover routing policy**.
 
### Improvement for existing solutions
- If you have existing solution with **CloudFront** with **partitioned data in AWS** and you want to **improve the load time**, then use **S3 bucket with partitioned data** and **CloudFront  distribution with access permissions to S3 and is restricted only to it**.
- If you need to **satisfy the RTO and RPO timeframes**, **improve the high availability, scalability and disaster resilience** for **database logs and trading transactions**, use **AWS Backup for AWS RDS with PITR (point-in-time recovery) option enabled and export logs to S3 with backups every 'n' minutes and cross-region replication enabled**. For more information, see [Disaster Recovery Demystified - RTO vs RPO](https://www.youtube.com/watch?v=wgvq9y8wwNQ).
- If you need to **meet the requirements of RPO in hours and RTO in minutes**, use **warm standby** DR strategy with **autoscaling groups** in backup regions. For more information, see [Plan for Disaster Recovery (DR)](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/plan-for-disaster-recovery-dr.html).
- If company needs to **provide an external auditor access to it's service logs in AWS (EC2, S3, DynamoDB)**, then **enable CloudTrail logging, create IAM user with read only permissions to the required AWS resources and then provide the access credentials to the auditor**.
- If you need to **deploy ML model locally and on-premises environment without Internet access**, then **use AWS IoT Greengrass**. For more information, see [What is AWS IoT Greengrass?](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html)
- If you need to improve **application performance and keep it cost-effective** with **stateless application and consistent workload**, use **Reserved EC2 instances with auto-scaling group max number exceeding the current setup**.
- If you need to **improve the image upload to S3 bucket from another region than the origin S3 bucket**, use **S3 Transfer Acceleration on the central S3 bucket**. 
- If you need to **host static content of the website and serve it to different users based on their device type**, use **S3 static website with CloudFront distribution and Lamda@Edge function to parse User-Agent HTTP to serve appropriate content**. For more information, see [Customize at the edge with Lambda@Edge](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/lambda-at-the-edge.html)
- If you need to **audit access log reports for services**, enable **AWS Cloud Trail**. **To query access log reports**, use **Amazon Athena**. 
- If you need **automated patching of your on-premise and cloud based instances**, with **least amount of efforts**, use **AWS Systems Manager Patch Manager** with **AWS Systems Manager Maintenance Windows** to **automate patch schedule**.
- If you need to **restrict access to your S3 bucket via CloudFront distribution**, use **create an Origin Access Control (OAC) and associate it with your CloudFront distribution**.
- If you need to **track historical changes to the security configurations of your resources** and **compliance auditing**, use **AWS Config**.
- If you need to **improve scalability and high-availability of stateless applications**, use **auto-scaling groups with ElastiCache Read replicas and AWS RDS mutli-AZ setup with read replicas**.
- If you need to **discover, classify and protect personally identifiable information (PII) data use Amazon Macie**.
- If you need to **stop, delete or terminate resources in separate AWS accounts**, then in **each of the accounts, generate cross-account roles that have full admin permissions while granting access for the master account**.
- If you need a **secure and better way of SSL processing** for the web servers and ensure that **application logs are securely stored**, use **CloudHSM to perform SSL transactions** and use **private S3 bucket with SSE encryption** enabled.