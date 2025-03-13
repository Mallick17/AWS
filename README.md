# Disaster Recovery of Workloads on AWS: Recovery in the Cloud

| Disaster Recovery Option | Description | Pros | Cons |
|--------------------------|-------------|------|------|
| **Backup & Restore** | Data is backed up to the cloud and restored when needed. | Simple, cost-effective | Slow recovery, only restores data, not services. |
| **Pilot Light** | Minimal infrastructure is always running in the cloud, which can be scaled quickly. | Faster recovery than Backup & Restore | Still requires scaling, may need manual intervention. |
| **Warm Standby** | Scaled-down version of the full production environment, always ready to scale up. | Faster recovery, always running in the cloud | Higher costs than Pilot Light, requires scaling. |
| **Multi-Site** | Full infrastructure is replicated across multiple cloud regions. | Near-zero downtime, full redundancy | Expensive, complex to manage. |

## Disaster Recovery (DR) in AWS
#### **Why You Need a DR Plan**
- **Pixar Story**: 
  - In 1998, a Pixar employee accidentally deleted 90% of *Toy Story 2*, but a backup was corrupted.
  - Luckily, a technical director had a full copy at home, which saved the film.
  - *Toy Story 2* went on to gross $500 million, and Pixar made $14 billion, highlighting the importance of having a disaster recovery plan.

#### **What is Disaster Recovery?**
- **Definition**: DR is about ensuring business continuity after an event disrupts service.
  ![image](https://github.com/user-attachments/assets/fad158db-ce18-4e9f-8a11-94d0f2a9f9b2)

- **Key Concepts**:
  - **Resiliency**: Comprising both disaster recovery (recovery after failure) and availability (prevention of failure).
  - **Availability**: Measures to ensure minimal service downtime.
  - **Disaster Recovery**: Focuses on recovering services after failure, e.g., after a flood or a region outage.
  - **Quote**: “Everything fails all the time” – Werner Vogels, CTO of AWS.

---

#### **Disaster Recovery vs. Availability**
![image](https://github.com/user-attachments/assets/8e1a3f6f-3c17-470d-a461-9b2372482917)

- **Disaster**: A significant event that prevents your application from fulfilling its function at its primary deployed location.
- **High Availability**: Prevents service loss through redundant architectures, e.g., multiple availability zones or regions.
- **Resiliency**: Involves both disaster recovery and high availability.

#### **AWS Regions and Availability Zones**
- **Regions**: AWS has 25 global regions (with more planned), each with multiple availability zones (AZs).
  - **AZs** are separate data centers with redundant power and networking, designed to handle failures such as power outages or disasters.
  - Disaster planning should consider natural, technical, and human-caused failures.

#### **Shared Responsibility Model for Resiliency**
- **AWS's Responsibility**: Infrastructure resiliency (e.g., multiple regions, availability zones).
- **Customer's Responsibility**: Ensuring the resiliency of their workloads using AWS services.
![image](https://github.com/user-attachments/assets/33fe3ead-f788-40f4-8bdc-9a7c2fb23ddb)
#### **AWS Shared Responsibility Model Explanation**
- AWS operates under a **shared responsibility model**, meaning that security and compliance responsibilities are divided between **AWS (the cloud provider)** and **the customer (cloud user).**
#### **1. AWS Responsibility – "Security OF the Cloud"**  
AWS is responsible for protecting the **infrastructure that runs all AWS services**. This includes:  

#### **🔹 Infrastructure Security**  
- **Compute** (e.g., EC2 instances, Lambda)  
- **Storage** (e.g., S3, EBS)  
- **Databases** (e.g., RDS, DynamoDB)  
- **Networking** (e.g., VPC, Direct Connect)  

#### **🔹 Physical & Hardware Security**  
- Protecting **AWS Global Infrastructure** (Regions, Availability Zones, and Edge Locations).  
- Ensuring **hardware security** (server maintenance, networking equipment).  
- Compliance with industry standards (ISO, SOC, PCI DSS, etc.).  

#### **🔹 Software & Service Security**  
- Patching and maintaining the underlying AWS infrastructure.  
- Managing physical security of data centers.  

---

#### **2. Customer Responsibility – "Security IN the Cloud"**  
Customers are responsible for securing their own **data, applications, and configurations** on AWS. This includes:  

#### **🔹 Data Security**  
- **Customer Data** – Encrypting and managing data securely.  
- **Client-side Data Encryption** – Implementing encryption before sending data to AWS.  
- **Server-side Encryption** – Using AWS services to encrypt data at rest.  

#### **🔹 Application & Identity Security**  
- Managing **IAM (Identity and Access Management)** permissions.  
- Implementing **Multi-Factor Authentication (MFA)** for users.  
- Securing applications running on AWS.  

#### **🔹 Network Security**  
- Configuring **firewalls, security groups, and VPC settings**.  
- Implementing **Network Traffic Protection** (encryption, integrity, and identity verification).  
- Managing **operating system updates and patches**.  

---
#### **Key Takeaways**  
- AWS **secures the infrastructure**, while **customers secure their applications and data**.
- AWS ensures **physical and hardware security**, but customers must handle **IAM, encryption, and application security**.
- It follows a **"shared security responsibility"** approach, meaning **misconfigurations on the customer side can lead to security breaches**.
   
---

## **Disaster Recovery Strategies**
![image](https://github.com/user-attachments/assets/f427d185-a89a-4121-8263-24ffb779405d)

### Comparison of different **Disaster Recovery (DR) strategies** in cloud computing, particularly for AWS (Amazon Web Services). These strategies are categorized based on two key parameters:  

1. **Recovery Point Objective (RPO):**  
   - Defines how much data loss is acceptable in case of a failure.  
   - A **lower RPO** means **less data loss**, while a **higher RPO** means the system can afford to lose more data.  
![image](https://github.com/user-attachments/assets/95354598-85f2-499c-bfe9-85b30d545378)


2. **Recovery Time Objective (RTO):**  
   - Defines how quickly a system should recover after a failure.  
   - A **lower RTO** means **faster recovery**, while a **higher RTO** means a longer downtime is acceptable.  
![image](https://github.com/user-attachments/assets/acc88c13-47ae-4a9d-81ea-0010f5b3531c)

---

### **1. Backup & Restore (Active/Passive)**
- **RPO / RTO: Hours**

**What it is:**
This is the simplest form of disaster recovery, where data is regularly backed up to the cloud. If something goes wrong (like data loss or system failure), you restore the data from the backup to get things up and running again.

**How it works:**
- Periodically, important data is copied and stored in a cloud storage service.
- If there's a disaster (e.g., hardware failure or accidental deletion), the data can be restored to the original or a new environment.

**Example:**
Imagine you're running a small e-commerce store and you back up customer orders and inventory data to the cloud every night. If the physical server where your data is stored crashes, you can restore the backup from the cloud to another server, and your business can get back online.

- **Description:**
  - This is the **simplest and most cost-effective** disaster recovery strategy.
  - Data is **regularly backed up** to AWS storage services such as **Amazon S3 (Simple Storage Service), Amazon Glacier, or AWS Backup**.
  - However, **no AWS resources are actively running** to support disaster recovery.
  - In case of a disaster, the **entire infrastructure must be provisioned and restored manually**, which takes time.
  - This strategy is ideal for **non-critical workloads** where downtime and data loss are acceptable.  
  ![photo-collage png](https://github.com/user-attachments/assets/9c701e45-7d32-4edd-8903-a4de57fceeb1)

- **Use Cases:**
  - Data archiving.
  - Systems that do not require immediate recovery.
  - Cost-sensitive applications.

- **Pros:**
  - **Lowest cost** ($).
  - Simple implementation.
  - Can be used for long-term data storage.

- **Cons:**
  - **Slowest recovery time** (RTO of hours).
  - Higher data loss risk (RPO of hours).
  - Requires manual intervention to restore services.
  - Recovery time can be slow (especially if large amounts of data need to be restored).
  - It doesn't keep your application or infrastructure running during the downtime (it’s just a data restore).
---

### **2. Pilot Light (Active/Passive)**
- **RPO / RTO: Tens of minutes**

**What it is:**
The Pilot Light approach keeps a minimal version of your critical infrastructure running in the cloud, which can be quickly scaled up in the event of a disaster. It’s like having a small "pilot light" that you can turn up to full power when needed.

**How it works:**
- Core components of your system (like databases and essential services) are always running in the cloud in a minimal state.
- When a disaster strikes, the system can be quickly expanded to fully restore services.

**Example:**
Suppose you run a web application and have its database running in the cloud with only essential parts of the application. If the on-premise server or primary system fails, the pilot light setup allows you to quickly scale up resources in the cloud to take over fully. Your application can be up and running within hours instead of days.
- **Description:**
  - In this strategy, **critical data and components** (such as databases) are **always available**, but the rest of the system is **dormant**.
  - Compute resources (like servers and application instances) **are not fully running**, but **can be quickly started** when needed.
  - Upon a disaster, additional AWS resources are **scaled up** to meet demand.
  - This method balances cost and recovery speed, making it faster than Backup & Restore but more economical than fully active systems.
  ![photo-collage png (1)](https://github.com/user-attachments/assets/7b394927-9fe2-48ed-95ba-e2a0abe5f117)

- **Use Cases:**
  - Applications that need **somewhat fast recovery** but do not require full-time redundancy.
  - Workloads where the **database must always be available**, but web and application servers can be provisioned later.

- **Pros:**
  - **Faster recovery** than Backup & Restore.
  - **Moderate cost** ($$).
  - Scalable—compute resources can be increased when required. Only critical systems are running in the cloud, so it's cost-effective.

- **Cons:**
  - **Still requires some manual intervention** to scale up infrastructure.
  - Slower than Warm Standby or Active/Active setups.

---

### **3. Warm Standby (Active/Passive)**
- **RPO / RTO: Minutes**

**What it is:**
The Warm Standby approach involves maintaining a scaled-down version of your full production environment in the cloud. This environment is always ready to scale up to full capacity when a disaster occurs.

**How it works:**
- A cloud environment with a copy of the production system is running, but not fully active.
- In the event of a disaster, this environment can be quickly scaled to handle full production traffic.

**Example:**
Imagine your company runs a global video streaming service. In normal circumstances, only a portion of your servers and services are running in the cloud at a lower capacity. If your main data center fails, you can quickly scale the cloud-based systems to handle the full traffic, ensuring minimal downtime.  
- **Description:**
  - A **scaled-down** but **fully functional** version of the production environment is **always running** in AWS.
  - The system is **continuously active** but operates at a **lower capacity**.
  - When a disaster occurs, AWS resources **scale up quickly** to handle full traffic.
  - This strategy is commonly used for **business-critical applications** that require **fast recovery** but not full redundancy.
  ![photo-collage png (2)](https://github.com/user-attachments/assets/10196eb2-e7a3-435c-8bc5-acb12f230887)

- **Use Cases:**
  - E-commerce platforms or SaaS applications that need **near-instant recovery**.
  - Businesses that want **automatic failover** without running a fully redundant infrastructure.

- **Pros:**
  - **Much faster recovery** than Backup & Restore or Pilot Light (RTO in minutes).
  - **No need for manual intervention** to start services.
  - **Balances cost and recovery speed** ($$$).
  - Faster recovery than Pilot Light because the environment is already up and running.
  - You don’t need to set everything up from scratch during a disaster.

- **Cons:**
  - **More expensive** than Backup & Restore and Pilot Light.
  - Requires **constant monitoring** to ensure readiness.
  - It still requires some scaling to meet full demand.
  - Slightly higher costs due to running some infrastructure.


---

### **4. Multi-site Active/Active (Fully Active)**
- **RPO / RTO: Real-time**

**What it is:**
The Multi-Site strategy involves running your entire application or system across multiple sites, both in the cloud and on-premises. All sites are active and continuously running, so if one site fails, the other site continues without disruption.

**How it works:**
- Your system is fully replicated across different geographic locations.
- In case of a failure, the traffic is automatically redirected to another site, ensuring there’s no downtime.

**Example:**
For a large online bank, they might run their application and services across multiple cloud regions and data centers. If one region or data center goes down, the traffic is automatically routed to another location. This approach ensures that the bank’s services are always available, even if there's a disaster.
- **Description:**
  - The **highest level of disaster recovery strategy**, where multiple sites (AWS regions or data centers) are **always running and actively handling traffic**.
  - **Zero downtime and near-zero data loss**, as requests are automatically routed to healthy instances.
  - If one site fails, another site immediately takes over without human intervention.
  - Used for **mission-critical applications** that require **100% availability**.
  ![Screenshot 2025-03-12 093343](https://github.com/user-attachments/assets/79b60c0c-3137-46f5-ab89-f871cc95ced7)

- **Use Cases:**
  - Global applications requiring **zero downtime** (e.g., social media platforms, banking systems).
  - High-traffic web applications with **customers worldwide**.
  - Services that cannot tolerate **any disruption**.

- **Pros:**
  - **Fastest recovery time (RTO = real-time)**.
  - **Lowest data loss (RPO = real-time)**.
  - Fully automated failover.
  - Ensures **high availability** and **business continuity**.

- **Cons:**
  - **Most expensive** disaster recovery option ($$$$) due to the need to run full infrastructure in multiple locations..
  - Requires **complex infrastructure** and advanced AWS services.

---

### **Comparison Summary**
| DR Strategy | RPO (Data Loss) | RTO (Recovery Time) | Cost | Best Use Case |
|-------------|---------------|----------------|------|----------------|
| **Backup & Restore** | Hours | Hours | $ | Low-priority applications, cost-sensitive environments |
| **Pilot Light** | Tens of minutes | Tens of minutes | $$ | Apps needing some live data but not full-time running |
| **Warm Standby** | Minutes | Minutes | $$$ | Business-critical apps needing quick failover |
| **Multi-site Active/Active** | Real-time | Real-time | $$$$ | Mission-critical applications needing zero downtime |

---

### **Final Thoughts**
- **Backup & Restore** is the simplest and cheapest but has the longest downtime.
- **Pilot Light** speeds up recovery by keeping **data live** but services idle.
- **Warm Standby** ensures **faster recovery** with a **partially running system**.
- **Multi-site Active/Active** is the **best for mission-critical systems** but has **the highest cost**.

Each approach is suited for different business needs based on **budget, downtime tolerance, and criticality of the application**. Companies often **mix multiple strategies** for different workloads to balance cost and availability.

#### **Common DR Strategies:**
1. **Backup and Restore**:
   - Simple, low-cost option.
   - Longer Recovery Point Objective (RPO) and Recovery Time Objective (RTO).
   - Example: Backing up EC2 instances, EBS volumes, and RDS instances across regions and restoring them after failure.

2. **Pilot Light**:
   - A minimal version of your environment is always running in a target region.
   - You scale up to full capacity after a disaster.
   - Example: Use of golden AMIs and Auto Scaling to restore workloads quickly.

3. **Warm Standby**:
   - A scaled-down version of the application is running continuously in the target region.
   - Traffic can be switched quickly in case of failure.
   - Example: RDS replicas, scaled EC2 instances in standby mode.

4. **Multi-Site Active-Active**:
   - Full environments are active in multiple regions at all times.
   - Both regions handle live traffic and can failover seamlessly.
   - Example: DynamoDB Global Tables for cross-region replication of data.

#### **Active-Passive vs. Active-Active**
- **Active-Passive**:
   - One region actively serves traffic, and the other remains a passive backup.
   - Failover happens when the active region goes down.
- **Active-Active**:
   - Both regions actively serve traffic, and failover occurs automatically or manually if one region fails.

#### **Considerations for DR Strategy**
- **Business Impact Analysis (BIA)**: Understand the criticality of workloads and determine acceptable downtime (RTO) and data loss (RPO).
- **Risk Assessment**: Account for natural, technical, and human risks.
- **Cost Consideration**: Ensure the DR strategy aligns with business requirements and budget.

#### **RPO and RTO**
- **RPO (Recovery Point Objective)**: Maximum acceptable data loss, typically measured by time.
- **RTO (Recovery Time Objective)**: Maximum acceptable downtime or delay between service failure and restoration.
- **Cost of Downtime**: Directly correlates to RTO; longer downtime equals higher costs.

---

### **Implementing DR in AWS**
1. **Backup and Restore**:
   - Use **AWS Backup** to centralize and automate backups across regions.
   - Restore with **CloudFormation** and **Lambda**.

2. **Pilot Light**:
   - Maintain a minimal version in the target region.
   - Use **Auto Scaling** and **Route 53** to handle failover.

3. **Warm Standby**:
   - Keep a reduced version of the system running in the target region.
   - Scale resources quickly after a disaster.

4. **Multi-Site Active-Active**:
   - Use **DynamoDB Global Tables** for data replication across regions.
   - Ensure both regions handle reads and writes for active traffic.

#### **Detection and Automation**
- Use **CloudWatch** and **Personal Health Dashboard** to detect failures automatically.
- **EventBridge** can alert operators and trigger automated recovery processes.

#### **Testing and Validation**
- Regularly test the DR strategy with simulated disaster recovery exercises (e.g., game days).
- Have clear **runbooks** to follow in case of an actual disaster.

---

### **Well-Architected Framework for DR**
- The **Well-Architected Framework** focuses on best practices across reliability, performance, cost, and security.
- Use the **Well-Architected Tool** to evaluate your workloads and generate improvement plans.

---

### **Summary**
- Align the DR strategy with business needs, cost, and recovery objectives.
- Use AWS tools (e.g., **AWS Backup**, **CloudFormation**, **Route 53**) to automate and manage your DR processes.
- Ensure ongoing testing and validation to ensure reliability in a disaster scenario.

---

### **Disaster Recovery Strategy Map**

Here’s a **Mind Map** that visually organizes the key components of the AWS disaster recovery strategies:

1. **Disaster Recovery (DR)**
   - **Types of DR**:
     - Backup & Restore
     - Pilot Light
     - Warm Standby
     - Multi-Site Active-Active
   - **Key Metrics**:
     - **RPO (Recovery Point Objective)**
     - **RTO (Recovery Time Objective)**
   - **AWS Services**:
     - **Route 53** (DNS Failover)
     - **DynamoDB Global Tables** (Cross-Region Replication)
     - **AWS Backup**
     - **CloudFormation**
     - **Auto Scaling**

2. **Availability Zones & Regions**
   - **Regions**: 25 global locations (with future plans)
   - **Availability Zones**: Isolated data centers within regions
   - **Considerations**: Geographical impact (local, regional, global disasters)

3. **DR Strategy Implementation**
   - **Active-Passive** vs **Active-Active**
   - **Backup Process**: Centralized backup using AWS services
   - **Testing**: Regular drills, runbooks, game days

4. **Costs and Risk Analysis**
   - **Cost of Downtime**: Increased with longer RTO
   - **Business Impact Analysis**: Understand how critical workloads affect your recovery strategy

---
