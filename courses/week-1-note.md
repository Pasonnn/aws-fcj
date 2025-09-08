# Week 1 – Network Foundation of AWS

This week focuses on the essential networking components in AWS that form the backbone for secure, high-performing, and highly available cloud applications. Understanding these concepts is crucial for building architectures that are scalable, resilient, and cost-efficient.

---

## 1. VPC and IP Addressing

An **Amazon VPC (Virtual Private Cloud)** is your isolated network environment in AWS.  
When creating a VPC, you must assign it a **CIDR block** — a range of IP addresses.

- **Recommended ranges (RFC 1918 private IPs):**
  - `10.0.0.0/8`
  - `172.16.0.0/12`
  - `192.168.0.0/16`

- **Constraints:**
  - VPC CIDR must be between `/16` (65,536 IPs) and `/28` (16 IPs).
  - You can associate **multiple CIDR blocks** with one VPC (primary + secondary).
  - Avoid **overlapping ranges** to allow smooth VPC peering or hybrid connectivity.

⚡ **Best practice:** Plan non-overlapping ranges across dev, staging, and prod to simplify future multi-VPC or hybrid networking.

---

## 2. Secure Hybrid Connectivity

To extend your data center into AWS:

- **AWS Site-to-Site VPN**  
  - Creates an encrypted **IPSec tunnel** between your on-premises network (via a **Customer Gateway**) and your AWS VPC (via a **Virtual Private Gateway** or **Transit Gateway**).  
  - Runs over the public internet, but remains fully encrypted.

- **AWS Direct Connect**  
  - Provides a **dedicated private line** to AWS.  
  - Lower latency, more consistent throughput, often used for enterprise-grade workloads.  
  - Can be paired with VPN for redundancy.

---

## 3. Subnets and Internet Access

- **Public Subnets**  
  - Have a route to an **Internet Gateway (IGW)**.  
  - Allow EC2 instances to have **direct internet access** (requires public IP or Elastic IP).

- **Private Subnets**  
  - No direct internet access.  
  - Use **NAT Gateway** in a public subnet for outbound internet connectivity (e.g., to fetch updates, call external APIs).  
  - NAT blocks all inbound connections from the internet.

---

## 4. VPC-to-VPC Communication

- **VPC Peering**
  - Direct connection between two VPCs.  
  - Works across accounts and regions.  
  - No transitive routing (A ↔ B and B ↔ C does not mean A ↔ C).  

- **AWS Transit Gateway (TGW)**
  - Hub-and-spoke model for connecting multiple VPCs and on-prem networks.  
  - Scales better than peering.  
  - Supports **transitive routing** and **cross-region peering**.

---

## 5. DNS and Global Traffic Management

- **Amazon Route 53**
  - AWS’s scalable DNS service.  
  - Supports:
    - **DNS failover** via health checks.  
    - **Geolocation-based routing** (direct users by location).  
    - **Latency-based routing** (reduce latency by sending users to the nearest healthy region).  
    - Weighted and multi-value routing policies.  

⚡ **High availability:** Achieved by combining routing policies with health checks.

---

## 6. Security at the Network Layer

- **Security Groups (SGs)**
  - Apply at the **Elastic Network Interface (ENI)** or instance level.  
  - **Stateful:** If inbound is allowed, response outbound is automatically allowed.  
  - Only support **allow rules**.  

- **Network ACLs (NACLs)**
  - Apply at the **subnet level**.  
  - **Stateless:** Must explicitly allow both inbound and outbound traffic.  
  - Support both **allow** and **deny rules**.  

⚡ **Key difference:**  
SGs = instance-level, stateful, allow-only.  
NACLs = subnet-level, stateless, allow + deny.

---

## 7. High Availability and Low Latency Deployment

- **Multi-AZ:** Always spread workloads across multiple Availability Zones in a region.  
- **Multi-Region:** Deploy active-active (preferred) or active-passive.  
- **Global data replication:**  
  - Use **DynamoDB Global Tables**, **Aurora Global Database**, or **S3 Cross-Region Replication**.  
- **Traffic routing:**  
  - Use **Route 53 latency-based routing**.  
  - Use **CloudFront CDN** for cached content close to end-users.  
- **Observability & Testing:**  
  - Regular chaos tests and health checks to validate failover.

---

## 8. Content Delivery

- **Amazon CloudFront**
  - AWS’s **Content Delivery Network (CDN)**.  
  - Caches static and dynamic content at **edge locations worldwide**.  
  - Integrates with S3, EC2, ALB, API Gateway.  
  - Improves performance, reduces latency, and adds an extra security layer with AWS Shield + WAF.

---

## 9. Monitoring and Traffic Visibility

- **VPC Flow Logs**
  - Capture metadata about IP traffic into/out of ENIs.  
  - Provide visibility for:
    - Troubleshooting (blocked traffic, routing issues).  
    - Security monitoring (unexpected ports or IPs).  
    - Compliance and auditing.  
    - Optimization (analyze usage patterns).  
  - Data stored in **CloudWatch Logs** or **S3**.

---

## 10. Redundancy in Hybrid Connectivity

- **Direct Connect Redundancy**
  - Deploy **multiple DX connections** across different devices and locations.  
  - Configure **BGP** for automatic failover (active-active or active-passive).  
  - Combine with a **VPN backup** for internet-based fallback.  

⚡ Ensures no single point of failure in hybrid connectivity.

---

# ✅ Summary

By the end of Week 1, you should understand:

- How VPCs are structured with CIDR blocks and subnets.  
- The role of **Internet Gateway**, **NAT Gateway**, and **Transit Gateway**.  
- How AWS ensures **secure hybrid connectivity** with VPN and Direct Connect.  
- How **Route 53** and **CloudFront** deliver global high availability and low latency.  
- The difference between **Security Groups** and **NACLs**.  
- How to monitor network traffic with **VPC Flow Logs**.  
- Why redundancy and multi-region design are essential for resilient architectures.  

This foundation sets you up for deeper dives into **advanced networking, security, and hybrid architectures** in AWS.

