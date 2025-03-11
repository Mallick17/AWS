# AWS
- Amazon Web Services, Inc. (AWS) is a subsidiary of Amazon that provides on-demand cloud computing platforms and APIs to individuals, companies, and governments, on a metered, pay-as-you-go basis. Clients will often use this in combination with autoscaling (a process that allows a client to use more computing in times of high application usage, and then scale down to reduce costs when there is less traffic).
- These cloud computing web services provide various services related to networking, compute, storage, middleware, IoT and other processing capacity, as well as software tools via AWS server farms.
- AWS's virtual computers emulate most of the attributes of a real computer, including hardware central processing units (CPUs) and graphics processing units (GPUs) for processing; local/RAM memory; hard-disk (HDD)/SSD storage; a choice of operating systems; networking; and pre-loaded application software such as web servers, databases, and customer relationship management (CRM).

## AWS Global Infrastructure
- The AWS Global Infrastructure is a globally distributed network designed to provide reliable, secure, and scalable cloud solutions. It consists of multiple regions and availability zones strategically located worldwide to minimize latency and ensure high availability. Businesses rely on the AWS Global Infrastructure to host their applications closer to their customers, enhancing performance and user satisfaction. With its robust design, the AWS Global Infrastructure supports redundancy, ensuring business continuity even during unexpected disruptions.
- AWS Global Infrastructure is the foundational architecture that supports Amazon Web Services (AWS) and enables the delivery of services worldwide. It is designed to provide high availability, fault tolerance, and low latency for applications.

### AWS Global Infrastructure Components
- Amazon Web Services (AWS) operates in a globally distributed cloud infrastructure to provide high availability, low latency, and fault tolerance. This infrastructure is built upon Regions, Availability Zones (AZs), Local Zones, Wavelength Zones, and Edge Locations.
  
1. **AWS Regions**
- AWS has the concept of a Region, which is a physical location around the world where we cluster data centers. We call each group of logical data centers an Availability Zone. Each AWS Region consists of a minimum of three, isolated, and physically separate AZs within a geographic area.
- An AWS Region is a geographically isolated area that contains multiple Availability Zones (AZs). Each AWS Region operates independently and has low-latency connectivity to other Regions.
- Each AWS Region consists of:
  - Multiple Availability Zones (AZs)
  - Regional Edge Caches
  - AWS Direct Connect

2. **Availability Zones (AZs)**
- An Availability Zone (AZ) is a physically separate data center within a Region. Each AZ has:
  - Independent power, cooling, and networking
  - Low-latency connectivity to other AZs in the same Region
  - Automatic failover and redundancy
![image](https://github.com/user-attachments/assets/7724111e-4ce5-47e8-bc96-da24a4a541ff)  

3. **Local Zones**
- "Local zone" (considered a "local edge" in this context) allows you to run your own compute workloads in a specific geographic area with extremely low latency, essentially bringing AWS services closer to the end user in major metropolitan cities; you cannot run your own workloads directly on an edge location, only use it for content delivery. 
- AWS Local Zones are designed to extend AWS services closer to end users in cities where no AWS Region exists. These zones provide low-latency computing for applications like gaming, live streaming, augmented reality (AR), and machine learning (ML).
- Local Zones provide a subset of AWS services to run workloads closer to end-users, while edge locations are primarily used for caching and accelerating content delivery.

4. **Wavelength Zones**
- AWS Wavelength Zones are built for 5G networks, enabling developers to run applications at ultra-low latency by placing compute and storage within telecom operator data centers. These are ideal for applications like autonomous vehicles, real-time gaming, and AR/VR.
  
5. **Edge Locations**
**Edge Locations** are the physical locations where AWS services like **Amazon CloudFront** and **AWS Global Accelerator** cache and deliver content closer to end users. These locations are part of a global network designed to reduce latency, improve performance, and optimize the delivery of content, such as web pages, media files, APIs, etc.

#### Key Points:
- **Purpose:** The primary goal of edge locations is to reduce the time it takes for data to travel across the internet from the source to the user.
- **How They Work:** Edge locations are strategically placed in different geographic regions worldwide, often in major cities or densely populated areas. When a user requests content (e.g., a website, video, or file), the request is routed to the nearest edge location. If the content is cached there, it's delivered quickly. If it's not cached, it will be fetched from the origin server and then cached at the edge for future use.
- **Example:** If you are using **Amazon CloudFront** (a Content Delivery Network service), when someone from London accesses your website, their request may be handled by an edge location in London (or a nearby city) rather than traveling to a central server in another part of the world (e.g., the U.S.).

6. **Local Edge Locations (AWS Local Zones)**

**Local Edge Locations** refer to a specific type of edge location known as **AWS Local Zones**. These are extensions of AWS Regions that are located closer to end-users and are designed to run low-latency applications where AWS's regular data centers (regions) may be too far away.

#### Key Points:
- **Purpose:** Local Zones are meant to support workloads that require single-digit millisecond latencies to end-users, such as real-time gaming, live video streaming, and edge computing.
- **Proximity to Users:** They are often placed in cities where demand for low-latency services is high, like Los Angeles, Boston, or Chicago in the U.S. These Local Zones bring AWS's compute, storage, and other services closer to end-users.
- **Example:** If you run a gaming application and need very fast processing and low latency for players in a certain area, using a **Local Zone** in that region can provide a better experience compared to using AWS's main data centers located farther away.

**Key Differences Between Edge Locations and Local Edge Locations:**

| **Aspect** | **Edge Locations** | **Local Edge Locations (AWS Local Zones)** |
|------------|--------------------|-------------------------------------------|
| **Purpose** | Content Delivery (caching data for low latency) | Low-latency processing for edge computing applications |
| **Services** | Primarily used for services like CloudFront, Route 53, Lambda@Edge | Compute, storage, and other AWS services closer to end-users |
| **Latency** | Reduces latency by caching content closer to users | Provides ultra-low latency for applications requiring fast processing |
| **Use Cases** | Content Delivery Network (CDN), DNS resolution | Real-time applications (gaming, video streaming), edge computing |

---
## AWS Global Infrastructure Architecture
- AWS infrastructure is designed in a layered architecture to maximize fault tolerance, scalability, and security.
- **AWS Regions**:
  - Independent cloud environments (geographically separate)
- **Availability Zones (AZs):**
  - Isolated data centers within a Region
- **Local Zones:**
  - Bring AWS services closer to users in large cities
- **Wavelength Zones:**
  - Enable ultra-low-latency applications for 5G networks
- **Edge Locations:**
  - Accelerate content delivery via AWS CloudFront

### **High-Level AWS Architecture Diagram**  

```pgsql
                         +-------------------------------------------------+
                         |               AWS Global Infrastructure         |
                         +-------------------------------------------------+
                                         /               \
         +-----------------------------------------------------------+
         |                      AWS Regions                           |
         +-----------------------------------------------------------+
              /       |        |        |        |        |        \
    +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+
    | Region | | Region | | Region | | Region | | Region | | Region | | Region |
    | (US)   | | (EU)   | | (Asia) | | (Canada)| | (SA)   | | (ME)   | | (China) |
    +-------+ +-------+ +-------+ +-------+ +-------+ +-------+ +-------+
              /       |        |        |        |        |        \
    +---------------------------------------------------------------+
    |                    Availability Zones (AZs)                    |
    |      (Data Centers with Compute, Storage, and Networking)      |
    +---------------------------------------------------------------+
              /       |        |        |        |        |        \
  +-------------------------------------------------------------+
  |   Local Zones  |    Wavelength Zones    |    Edge Locations  |
  +-------------------------------------------------------------+
        |                     |                         |
        |                     |                         |
  +------------------------------------+         +----------------------+
  |       Customer Applications        |         |  AWS Services (CDN)  |
  +------------------------------------+         +----------------------+
```


## **AWS Regions and Availability Zones (AZs)**  
- The AWS Cloud spans 114 Availability Zones within 36 geographic regions, with announced plans for 12 more Availability Zones and four more AWS Regions in New Zealand, the Kingdom of Saudi Arabia, Taiwan, and the AWS European Sovereign Cloud.
  
### **North America**  
- The AWS Cloud in North America has 28 Availability Zones within eight geographic Regions, with 44 Edge Network locations and two Regional Edge Cache locations.
  
<details>
  <summary>Click to View North America Region</summary>

| **Region**              | **Availability Zones (AZs)**                                                                 | **Local Zones**                                                                                              | **Wavelength Zones**                           |
|-------------------------|----------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| **Northern Virginia**   | `us-east-1a`, `us-east-1b`, `us-east-1c`, `us-east-1d`, `us-east-1e`, `us-east-1f`                      | Atlanta, Boston, Chicago, Dallas, Denver, Houston, Kansas City, Las Vegas, Los Angeles, Miami, Minneapolis, New York City, Philadelphia, Phoenix, Portland, Seattle | Boston, Chicago, Dallas, Denver, Los Angeles, Miami, New York City, San Francisco |
| **Ohio**               | `us-east-2a`, `us-east-2b`, `us-east-2c`                                                           | -                                                                                                            | -                                              |
| **Northern California** | `us-west-1a`, `us-west-1b`, `us-west-1c`                                                           | -                                                                                                            | -                                              |
| **Oregon**             | `us-west-2a`, `us-west-2b`, `us-west-2c`, `us-west-2d`                                               | Los Angeles, Las Vegas, Phoenix, Salt Lake City, Seattle, Portland, Denver                                   | San Francisco, Seattle                         |
| **AWS GovCloud (US-East)** | `us-gov-east-1a`, `us-gov-east-1b`, `us-gov-east-1c`                                         | -                                                                                                            | -                                              |
| **AWS GovCloud (US-West)** | `us-gov-west-1a`, `us-gov-west-1b`, `us-gov-west-1c`                                         | -                                                                                                            | -                                              |
| **Canada Central**     | `ca-central-1a`, `ca-central-1b`, `ca-central-1c`                                                  | -                                                                                                            | -                                              |
| **Canada West**        | `ca-west-1a`, `ca-west-1b`, `ca-west-1c`                                                            | -                                                                                                            | -                                              |
| **Mexico (Central)**   | `mx-central-1a`, `mx-central-1b`, `mx-central-1c`                                                  | -                                                                                                            | -                                              |

#### **Edge Locations in North America**  
- **USA:** Ashburn (VA), Atlanta (GA), Boston (MA), Chicago (IL), Columbus (OH), Dallas/Fort Worth (TX), Denver (CO), Houston (TX), Jacksonville (FL), Kansas City (MO), Los Angeles (CA), Miami (FL), Minneapolis (MN), Nashville (TN), New York (NY), Newark (NJ), Philadelphia (PA), Phoenix (AZ), Portland (OR), Salt Lake City (UT), San Jose (CA), Seattle (WA), South Bend (IN), St. Louis (MO), Tampa Bay (FL), Washington D.C.  
- **Canada:** Montreal (QC), Toronto (ON)  
- **Mexico:** Queretaro  

#### **Regional Edge Caches in North America**  
- **Northern Virginia, Ohio, Oregon**  

</details>

---

### **Asia Pacific & China** 
- The AWS Cloud in Asia Pacific and China has 44 Availability Zones within 14 geographic Regions, with 34 Edge Network locations and 5 Regional Edge Cache locations.

<details>
  <summary>Click to View Asia Pacific & China Region</summary>
  
| **Region**            | **Availability Zones (AZs)**                                                             | **Local Zones** | **Wavelength Zones**  |
|----------------------|------------------------------------------------------------------------------------------|-----------------|-----------------------|
| **Beijing**         | `cn-north-1a`, `cn-north-1b`, `cn-north-1c`                                                    | -               | -                     |
| **Hong Kong SAR**   | `ap-east-1a`, `ap-east-1b`, `ap-east-1c`                                                       | -               | -                     |
| **Hyderabad**       | `ap-south-2a`, `ap-south-2b`, `ap-south-2c`                                                    | -               | -                     |
| **Jakarta**         | `ap-southeast-3a`, `ap-southeast-3b`, `ap-southeast-3c`                                        | -               | -                     |
| **Malaysia**        | `ap-southeast-4a`, `ap-southeast-4b`, `ap-southeast-4c`                                        | -               | -                     |
| **Melbourne**       | `ap-southeast-5a`, `ap-southeast-5b`, `ap-southeast-5c`                                        | -               | -                     |
| **Mumbai**         | `ap-south-1a`, `ap-south-1b`, `ap-south-1c`                                                     | Chennai, Kolkata | -                     |
| **Ningxia**        | `cn-northwest-1a`, `cn-northwest-1b`, `cn-northwest-1c`                                         | -               | -                     |
| **Osaka**          | `ap-northeast-3a`, `ap-northeast-3b`, `ap-northeast-3c`                                         | -               | -                     |
| **Seoul**          | `ap-northeast-2a`, `ap-northeast-2b`, `ap-northeast-2c`, `ap-northeast-2d`                        | -               | Seoul                 |
| **Singapore**      | `ap-southeast-1a`, `ap-southeast-1b`, `ap-southeast-1c`                                         | Jakarta         | -                     |
| **Sydney**         | `ap-southeast-2a`, `ap-southeast-2b`, `ap-southeast-2c`                                         | Perth, Brisbane | -                     |
| **Thailand**       | `ap-southeast-6a`, `ap-southeast-6b`, `ap-southeast-6c`                                         | Bangkok         | -                     |
| **Tokyo**          | `ap-northeast-1a`, `ap-northeast-1b`, `ap-northeast-1c`, `ap-northeast-1d`                        | Osaka           | Tokyo                 |

#### **Edge Locations in Asia Pacific & China**  
- **Australia:** Brisbane, Melbourne, Perth, Sydney  
- **China:** Beijing, Shanghai, Zhongwei, Shenzhen  
- **India:** Bangalore, Chennai, Hyderabad, Kolkata, Mumbai, New Delhi, Pune  
- **Indonesia:** Jakarta  
- **Japan:** Osaka, Tokyo  
- **Malaysia:** Kuala Lumpur  
- **New Zealand:** Auckland  
- **Philippines:** Manila  
- **South Korea:** Seoul  
- **Taiwan:** Taipei  
- **Thailand:** Bangkok  
- **Vietnam:** Hanoi, Ho Chi Minh City  

#### **Regional Edge Caches in Asia Pacific & China**  
- **Mumbai, Singapore, Seoul, Tokyo, Sydney**  

</details>

---

### **South America**  
- The AWS Cloud in South America has 3 Availability Zones within one geographic Region, with four Edge Network locations and one Regional Edge Cache location.

<details>
  <summary>Click to View South America Region</summary>

| **Region**         | **Availability Zones (AZs)**  |
|-------------------|----------------------------|
| **São Paulo**    | `sa-east-1a`, `sa-east-1b`, `sa-east-1c` |

#### **Edge Locations in South America**  
- **Argentina:** Buenos Aires  
- **Brazil:** Fortaleza, Rio de Janeiro, São Paulo  
- **Chile:** Santiago  
- **Colombia:** Bogotá  
- **Peru:** Lima  

#### **Regional Edge Caches in South America**  
- **São Paulo**  

</details>

---

### **Europe, Middle East & Africa**  
- The AWS Cloud in Europe, Middle East and Africa has 36 Availability Zones within 12 geographic Regions, with 39 Edge Network locations and two Regional Edge Cache locations.

<details>
  <summary>Click to View Europe, Middle East & Africa Region</summary>

| **Region**       | **Availability Zones (AZs)** | **Local Zones** | **Wavelength Zones**  |
|-----------------|-----------------------------|-----------------|-----------------------|
| **Bahrain**    | `me-south-1a`, `me-south-1b`, `me-south-1c` | Manama | - |
| **Cape Town**  | `af-south-1a`, `af-south-1b`, `af-south-1c` | Johannesburg | - |
| **Frankfurt**  | `eu-central-1a`, `eu-central-1b`, `eu-central-1c` | Hamburg, Berlin | - |
| **Ireland**    | `eu-west-1a`, `eu-west-1b`, `eu-west-1c` | - | - |
| **London**     | `eu-west-2a`, `eu-west-2b`, `eu-west-2c` | - | London |
| **Paris**      | `eu-west-3a`, `eu-west-3b`, `eu-west-3c` | - | - |
| **Stockholm**  | `eu-north-1a`, `eu-north-1b`, `eu-north-1c` | - | - |

#### **Edge Locations in Europe, Middle East & Africa**  
- **Cities:** Amsterdam, Berlin, Dubai, Frankfurt, Johannesburg, London, Madrid, Paris, Stockholm, Tel Aviv, Zurich  

#### **Regional Edge Caches in Europe, Middle East & Africa**  
- **Frankfurt, London**  

</details>

---

## **AWS Infrastructure Benefits**  

AWS provides a highly **resilient, scalable, and low-latency** cloud infrastructure. Key benefits include:  

1. **Fault Tolerance:** Multiple AZs prevent downtime due to hardware failures.  
2. **Low Latency:** Edge Locations and Wavelength Zones ensure fast content delivery.  
3. **Scalability:** Auto Scaling, Elastic Load Balancing, and AWS Global Accelerator optimize performance.  
4. **Security & Compliance:** AWS follows industry security standards like **ISO 27001, SOC 2, HIPAA, and GDPR**.  

---

