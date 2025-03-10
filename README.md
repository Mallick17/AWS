## AWS Pricing Models

| **Pricing Model**       | **Discounts**            | **Commitment**        | **Best for**                          |
|-------------------------|--------------------------|-----------------------|---------------------------------------|
| **On-Demand**            | No discount              | No commitment         | Short-term, unpredictable workloads  |
| **Reserved Instances**   | Up to 72%                | 1 or 3 years          | Predictable, long-term workloads     |
| **Spot Instances**       | Up to 90%                | No commitment         | Non-critical, flexible workloads     |
| **Savings Plans**        | Up to 72%                | 1 or 3 years          | Predictable workloads with flexibility|
| **Free Tier**            | Free up to usage limits  | No commitment         | Learning, testing, non-production    |

### Pricing Model in Detail Summary:

<details>
  <summary>Click to view summary of Pricing Model -- Description -- Use Cases -- Key Services</summary>

| Pricing Model                                  | Description                                                                 | Key Services                    | Use Cases                                              |
|-----------------------------------------------|---------------------------------------------------------------------------|---------------------------------|-------------------------------------------------------|
| **Pay-as-You-Go**                              | Pay only for what you use without long-term contracts or upfront commitments. Charges are based on actual consumption. | EC2, Lambda, S3, RDS           | Variable workloads, unpredictable traffic, and new projects. |
| **Reserved Instances (Save When You Commit)**  | Get discounts by committing to use a service for 1 or 3 years. Reserved instances offer cost savings compared to on-demand pricing. | EC2, RDS, DynamoDB, ElastiCache | Steady-state workloads with predictable usage.        |
| **Spot Instances**                             | Purchase unused compute capacity at discounted rates, with the caveat that instances can be interrupted by AWS when they need the capacity back. | EC2, ECS                        | Fault-tolerant workloads, batch jobs, or flexible workloads. |
| **Savings Plans**                              | Commitment-based pricing model where you commit to a certain amount of usage ($/hour) in exchange for lower costs across specific AWS services. | EC2, Fargate, Lambda           | Long-term projects, committed resource needs over time. |
| **Free Tier**                                  | Allows users to explore AWS for free, with 12-months of free services, always free offerings, and free trials for some products. | EC2, S3, Lambda, RDS           | Test and development, small-scale usage, learning AWS. |
| **On-Demand Instances**                        | Pay for compute or database capacity with no long-term commitments or upfront payments. Cost depends on hourly or per-second usage. | EC2, RDS                        | Short-term, spiky, or unpredictable workloads.        |
| **Dedicated Hosts**                            | Physical servers dedicated for your use. Offers compliance benefits by allowing control over server-bound software licenses. | EC2                             | Licensing-heavy or compliance-based environments.      |
| **Data Transfer Pricing**                      | Charges for data transfer vary based on the source, destination, and transfer region (e.g., data in is free, data out incurs charges). | S3, EC2, CloudFront             | Heavy data transfer workloads, cross-region application setups. |
| **Elastic Block Store (EBS) Pricing**          | Pricing based on storage amount, provisioned IOPS, and throughput for attached EBS volumes. | EBS                             | Block storage for applications that require high throughput. |
| **Object Storage Pricing**                     | Pricing for S3 varies based on storage class (Standard, IA, Glacier) and amount of data stored and retrieved. | S3, Glacier                     | Static content storage, backup, and archival.        |

</details>

---

### 1. **On-Demand Instances**

#### Description:
- **On-Demand** allows you to pay for computing resources (like EC2 instances) on an hourly or per-second basis, without any long-term commitments.
- This is the **default pricing model** for AWS EC2 compute services.
- You pay for the compute capacity used while the instance is running.

#### Pros:
- **Pay-as-you-go model**: You only pay for what you use (per hour/second).
- **No long-term commitment**: You can start and stop instances at will.
- **High flexibility**: Ideal for unpredictable workloads or short-term projects.
  
#### Cons:
- **Expensive**: It is one of the most expensive pricing models for long-term workloads.
- **Not suitable for long-running production instances**: There are cheaper options (Reserved Instances or Savings Plans) for long-term use.

#### When to Use:
- **Short-term projects** (e.g., Proof of Concepts, testing, and performance evaluations).
- **Unpredictable workloads** where capacity needs are not easily forecasted.

---

### 2. **Reserved Instances (RIS)**

#### Description:
- Reserved Instances involve a commitment to use EC2 instances for a **1 or 3-year term**.
- Users can pay in three ways: **All upfront**, **Partial upfront**, or **No upfront**.
- Reserved Instances offer **up to 72% discounts** compared to on-demand pricing, depending on the payment option.
- You can also opt for **Convertible RIS** which allows flexibility in instance types, as long as the new instance value is equal or greater.

#### Pros:
- **Discounts up to 72%**: Significant savings compared to on-demand pricing.
- **Predictable pricing**: Costs are fixed for the term of the commitment.
- **Guaranteed capacity**: Unlike on-demand, you are guaranteed capacity for the chosen instance.

#### Cons:
- **Reduced flexibility**: Requires a commitment for 1 to 3 years.
- **Limited options for changing instances**: Instance types and configurations can be difficult to modify.

#### When to Use:
- **Long-term use**: For predictable production applications or workloads with consistent resource requirements.
- **Stable workloads** where usage is predictable over time.

---

### 3. **Savings Plans**

#### Description:
- Savings Plans are a flexible pricing model that provides **up to 72% discount** on EC2, Lambda, and other services in exchange for a 1 or 3-year commitment.
- There are two types of Savings Plans:
  - **Compute Savings Plan**: The most flexible, offering savings across a range of EC2 instance families, regions, and even Fargate.
  - **EC2 Instance Savings Plan**: Offers higher discounts but requires commitment to a specific EC2 instance family and region.

#### Pros:
- **Flexible**: The Compute Savings Plan allows for changes in instance types and regions.
- **Up to 72% discount**: Savings can be substantial for users with predictable workloads.
- **Easy to manage**: More straightforward than Reserved Instances or Spot.

#### Cons:
- **Requires commitment**: You must commit to a certain amount of compute usage over a 1 or 3-year period.
- **On-demand pricing for excess usage**: If your usage exceeds the committed amount, it is billed at on-demand rates.

#### When to Use:
- **Predictable workloads**: For continuous workloads that are consistent and predictable, such as EC2, Fargate, or Lambda workloads.
- **Flexible and long-term needs**: When you want savings but also need flexibility in instance types and regions.

---
### 4. **Spot Instances**

#### Description:
- Spot Instances allow users to bid on unused EC2 capacity, potentially saving up to **90%** compared to on-demand pricing. AWS offers these instances at a lower cost since they are using excess capacity.
- AWS can terminate a Spot instance with only **2 minutes' notice** if the capacity is needed for on-demand or reserved instances.

#### Pros:
- **Cheapest option**: Discounts of up to 90% make it highly cost-effective for flexible workloads.
- **Great for non-critical workloads**: Ideal for tasks that can tolerate interruptions.

#### Cons:
- **Risk of termination**: AWS may terminate instances with minimal notice (2 minutes).
- **Complex setup**: Spot instances require more configuration and management, making them less beginner-friendly.

#### When to Use:
- **Non-critical or stateless workloads** (e.g., batch processing, ETL jobs, or analytics).
- **Flexible workloads** that can be restarted if terminated, such as data processing tasks.

---
<details>
  <summary>Key Differences and Common Features inbetween REserved Instances and Savings Plan</summary>


### **Key Differences Between Reserved Instances and Savings Plans**

| **Aspect**                  | **Reserved Instances (RIs)**                                  | **Savings Plans**                                                  |
|-----------------------------|---------------------------------------------------------------|--------------------------------------------------------------------|
| **Commitment Type**          | Commitment to a specific **instance type**, **region**, and **availability zone** (for standard RIs). | Commitment to a **dollar amount** of usage over a time period (1 or 3 years). Not tied to specific instance types. |
| **Flexibility**              | **Low flexibility**. Once committed, you're locked into specific instance types and regions. | **High flexibility**. Can be applied to different instance types, regions, and services. |
| **Applicable Services**      | Primarily for **EC2 instances** (including specific instance types). | Applies to a broader range of services including **EC2**, **Lambda**, **Fargate**, and **SageMaker**. |
| **Discounts**                | Typically offers a discount of **30-60%** compared to On-Demand pricing. | Offers discounts of **up to 72%** for EC2 instances (varies by plan type), with slightly lower discounts for other services (e.g., Lambda and Fargate). |
| **Payment Options**          | Available with **3 payment options**: 
   - All Upfront
   - Partial Upfront
   - No Upfront |
   | Available with **3 payment options**: 
   - All Upfront
   - Partial Upfront
   - No Upfront |
| **Changes After Purchase**   | Difficult to modify after purchase. Reserved Instances cannot easily be changed, and you may be locked into your commitment unless you sell the reserved instances on the **Reserved Instance Marketplace**. | More flexible. You can change the instance type, region, or even switch between services like EC2, Lambda, Fargate, etc., within your committed dollar amount. |
| **Term Length**              | Reserved Instances are available with **1-year** or **3-year** terms. | Savings Plans also have **1-year** or **3-year** terms. |
| **Instance Family & Size**   | Specific to an **instance family** (e.g., M5, C5) and size (e.g., m5.large, c5.xlarge) when using Standard RIs. | No instance type or size restrictions. Applicable across instance families and sizes. |
| **Scope**                    | Tied to a **specific region** and **availability zone** for standard RIs, which limits their application. | Can apply to all regions and availability zones, offering much broader flexibility. |
| **Instance Termination**     | **No automatic termination**. You are still billed even if you don’t use the Reserved Instance. | **No termination** for savings plans, and you only pay for what you commit to using. |  
</details>

### 5. **Free Tier**

#### Description:
- AWS provides a **Free Tier** which includes three types of offerings:
  - **Free Trial**: Short-term trials of various services.
  - **12-month Free Tier**: Free usage for 12 months after sign-up (e.g., EC2, S3, Lambda).
  - **Always Free**: Some services are free indefinitely, but with usage limits (e.g., AWS Lambda, DynamoDB).

#### Pros:
- **Free for 12 months**: Up to 750 hours per month for EC2, 5GB of S3 storage, and other offerings.
- **Always free services**: Some services like AWS Lambda and DynamoDB are free indefinitely with certain limits.
- **Ideal for testing and learning**: Great for experimenting with AWS services and learning the platform.

#### Cons:
- **Impractical for production**: The Free Tier is not designed for large-scale production use, especially for enterprise applications.
- **Usage limits**: Services are free only up to certain limits; exceeding those limits results in charges at standard rates.

#### When to Use:
- **Learning and testing**: Ideal for small projects, Proof of Concepts (POCs), or if you want to explore AWS services without incurring costs.
- **Non-production applications**: Running small websites or applications without large-scale resource needs.

---



### Scaling Flexibility:
- **On-Demand Instances** provide the most flexible scaling options, allowing you to scale up and down without restrictions, making them ideal for dynamic workloads.
- **Spot Instances** allow for scaling up quickly but have the risk of interruptions, making them more suitable for workloads that can tolerate instance termination.
- **Reserved Instances** offer the least flexibility for scaling as they require a long-term commitment, but they can still work for predictable, steady workloads with minimal scaling needs.
- **Savings Plans** strike a balance between flexibility and cost savings, allowing you to scale up and down within your commitment, but you'll need to meet the dollar commitment regardless of instance usage.

Thus, if **flexible scaling** is a priority, **On-demand Instances** and **Savings Plans** (to a lesser extent) are the best options. **Spot Instances** offer the lowest cost, but scaling down and dealing with interruptions can be challenging. **Reserved Instances** are best for highly predictable workloads where scaling changes are minimal.

---

### Conclusion:
- AWS offers diverse pricing models catering to different needs: **On-Demand** for flexibility, **Reserved Instances** for long-term savings, **Spot Instances** for cost-sensitive, non-critical workloads, and **Savings Plans** for predictable usage with flexibility.
- The **Free Tier** is perfect for small-scale testing and learning. 

