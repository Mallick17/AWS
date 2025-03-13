# Disaster Recovery of Workloads on AWS: Recovery in the Cloud
## Disaster Recovery (DR) in AWS
#### **Why You Need a DR Plan**
- **Pixar Story**: 
  - In 1998, a Pixar employee accidentally deleted 90% of *Toy Story 2*, but a backup was corrupted.
  - Luckily, a technical director had a full copy at home, which saved the film.
  - *Toy Story 2* went on to gross $500 million, and Pixar made $14 billion, highlighting the importance of having a disaster recovery plan.

#### **What is Disaster Recovery?**
- **Definition**: DR is about ensuring business continuity after an event disrupts service.
- **Key Concepts**:
  - **Resiliency**: Comprising both disaster recovery (recovery after failure) and availability (prevention of failure).
  - **Availability**: Measures to ensure minimal service downtime.
  - **Disaster Recovery**: Focuses on recovering services after failure, e.g., after a flood or a region outage.
  - **Quote**: “Everything fails all the time” – Werner Vogels, CTO of AWS.

---

#### **Disaster Recovery vs. Availability**
![resiliency-objectives](https://github.com/user-attachments/assets/22045152-a607-4945-8318-0d7b48ecf667)

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

---

## **Disaster Recovery Strategies**
![image](https://github.com/user-attachments/assets/f427d185-a89a-4121-8263-24ffb779405d)

### Comparison of different **Disaster Recovery (DR) strategies** in cloud computing, particularly for AWS (Amazon Web Services). These strategies are categorized based on two key parameters:  

1. **Recovery Point Objective (RPO):**  
   - Defines how much data loss is acceptable in case of a failure.  
   - A **lower RPO** means **less data loss**, while a **higher RPO** means the system can afford to lose more data.  
  ![image](https://github.com/user-attachments/assets/d8f4025f-a757-4941-b625-246d96b9ace2)

2. **Recovery Time Objective (RTO):**  
   - Defines how quickly a system should recover after a failure.  
   - A **lower RTO** means **faster recovery**, while a **higher RTO** means a longer downtime is acceptable.  
  ![image](https://github.com/user-attachments/assets/e154a514-0bd5-43e6-bfb1-85868f600ce2)

The image divides the DR strategies into **Active/Passive** and **Active/Active** approaches.  

---

### **1. Backup & Restore (Active/Passive)**
- **RPO / RTO: Hours**  
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

---

### **2. Pilot Light (Active/Passive)**
- **RPO / RTO: Tens of minutes**  
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
  - Scalable—compute resources can be increased when required.

- **Cons:**
  - **Still requires some manual intervention** to scale up infrastructure.
  - Slower than Warm Standby or Active/Active setups.

---

### **3. Warm Standby (Active/Passive)**
- **RPO / RTO: Minutes**  
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

- **Cons:**
  - **More expensive** than Backup & Restore and Pilot Light.
  - Requires **constant monitoring** to ensure readiness.

---

### **4. Multi-site Active/Active (Fully Active)**
- **RPO / RTO: Real-time**  
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
  - **Most expensive** disaster recovery option ($$$$).
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
