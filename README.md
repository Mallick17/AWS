# AWS
- Amazon Web Services, Inc. (AWS) is a subsidiary of Amazon that provides on-demand cloud computing platforms and APIs to individuals, companies, and governments, on a metered, pay-as-you-go basis. Clients will often use this in combination with autoscaling (a process that allows a client to use more computing in times of high application usage, and then scale down to reduce costs when there is less traffic).
- These cloud computing web services provide various services related to networking, compute, storage, middleware, IoT and other processing capacity, as well as software tools via AWS server farms.
- AWS's virtual computers emulate most of the attributes of a real computer, including hardware central processing units (CPUs) and graphics processing units (GPUs) for processing; local/RAM memory; hard-disk (HDD)/SSD storage; a choice of operating systems; networking; and pre-loaded application software such as web servers, databases, and customer relationship management (CRM).

## AWS Global Infrastructure
- The AWS Global Cloud Infrastructure is a secure, extensive, and reliable cloud infrastructure, offering over 200 fully featured services from data centers globally. Whether you need to deploy your application workloads across the globe in a single step or you want to build and deploy specific applications closer to your end users with single-digit millisecond latency, AWS provides you the cloud infrastructure where and when you need it.
- With millions of active customers and tens of thousands of partners globally, AWS has the largest and most dynamic community. Customers across virtually every industry and of every size, including start-ups, enterprises, and public sector organizations, are running every imaginable use case on AWS.
- **AWS Global Infrastructure Map**
  - The AWS Cloud spans 114 Availability Zones within 36 geographic regions, with announced plans for 12 more Availability Zones and four more AWS Regions in New Zealand, the Kingdom of Saudi Arabia, Taiwan, and the AWS European Sovereign Cloud.

---

## **AWS Regions and Availability Zones (AZs)**  

### **North America**  
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

---

### **Asia Pacific & China**  
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

---

### **South America**  
| **Region**         | **Availability Zones (AZs)**  |
|-------------------|----------------------------|
| **São Paulo**    | sa-east-1a, sa-east-1b, sa-east-1c |

#### **Edge Locations in South America**  
- **Argentina:** Buenos Aires  
- **Brazil:** Fortaleza, Rio de Janeiro, São Paulo  
- **Chile:** Santiago  
- **Colombia:** Bogotá  
- **Peru:** Lima  

#### **Regional Edge Caches in South America**  
- **São Paulo**  

---

### **Europe, Middle East & Africa**  
| **Region**       | **Availability Zones (AZs)** | **Local Zones** | **Wavelength Zones**  |
|-----------------|-----------------------------|-----------------|-----------------------|
| **Bahrain**    | me-south-1a, me-south-1b, me-south-1c | Manama | - |
| **Cape Town**  | af-south-1a, af-south-1b, af-south-1c | Johannesburg | - |
| **Frankfurt**  | eu-central-1a, eu-central-1b, eu-central-1c | Hamburg, Berlin | - |
| **Ireland**    | eu-west-1a, eu-west-1b, eu-west-1c | - | - |
| **London**     | eu-west-2a, eu-west-2b, eu-west-2c | - | London |
| **Paris**      | eu-west-3a, eu-west-3b, eu-west-3c | - | - |
| **Stockholm**  | eu-north-1a, eu-north-1b, eu-north-1c | - | - |

#### **Edge Locations in Europe, Middle East & Africa**  
- **Cities:** Amsterdam, Berlin, Dubai, Frankfurt, Johannesburg, London, Madrid, Paris, Stockholm, Tel Aviv, Zurich  

#### **Regional Edge Caches in Europe, Middle East & Africa**  
- **Frankfurt, London**  

---

