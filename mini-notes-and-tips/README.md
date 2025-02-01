# Mini notes and tips

These short notes and tips will help you to eliminate the wrong options and choose the correct answer(s).

## AWS Solutions Architect Pro

### Migrations

- If you want to migrate applications and workloads from on-premises to the cloud in **cost-effective** way, then use - **[AWS Application Migration Service](https://tutorialsdojo.com/aws-application-migration-service/)**. It uses **lift and shift** strategy.
- If you want to migrate workloads from on-premises to the cloud in a **faster way**, use **[AWS Direct Connect Service](https://tutorialsdojo.com/aws-direct-connect/)**. However, it can be **costly**. It uses **private network of AWS** to transfer data. 
- Use **[AWS VM Import/Export](https://aws.amazon.com/ec2/vm-import/)** service for **cost-effective** migration of servers from on-premises to the cloud. As this service, do not charge for import/export operation, beyond standard charges for EC2 and S3 services. 

### Desing a new solution
- If you need a service to **orchestrate** your workloads and that is **serverless**, use [**Step Functions**](https://tutorialsdojo.com/aws-step-functions/) with **Lambda**. This allows to **minimize the operational overhead**.
- If you need to **limit outbound web connections from your VPC to the internet** and **filter requests based on URLs**, then **use a forward web proxy** with custom domain whitelists or DNS content filtering services. For more information, see [How to set up an outbound VPC proxy with domain whitelisting and content filtering](https://aws.amazon.com/blogs/security/how-to-set-up-an-outbound-vpc-proxy-with-domain-whitelisting-and-content-filtering/)
- If you need to achieve **better availability and bandwidth with minimal efforts** to setup **Internet connection**, use **NAT Gateways** instead of NAT Devices. For more information, see [Compare NAT gateways and NAT instances](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html)
- If you need a **scalable solution** that can **handle a sudden spikes in traffic** use **CloudFront**, **Elstic Load Balancer**, **SQS** and **AutoScaling**. 