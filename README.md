# Disaster Recovery of Workloads on AWS: Recovery in the Cloud
### Detailed Notes on Disaster Recovery (DR) in AWS
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

### **Disaster Recovery Strategies**
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
