# Creating-and-configuring-a-network-load-balancer-in-AWS
# AWS Lab: Creating and Configuring a Network Load Balancer (NLB)

## Overview
This lab demonstrates how to create and configure an **AWS Network Load Balancer (NLB)** to distribute traffic across multiple EC2 instances.

The goal is to understand how AWS handles **high-performance, low-latency traffic at the transport layer (TCP/UDP)** and how load balancing improves availability and scalability.

---

## Architecture
## 🏗️ Architecture

```text
                    Internet
                        |
                        v
             +------------------------+
             |  Network Load Balancer |
             |         (NLB)          |
             +-----------+------------+
                         |
              -------------------------
              |                       |
              v                       v
      +---------------+       +---------------+
      |   EC2 Instance |       |   EC2 Instance |
      |    Target 1    |       |    Target 2    |
      +---------------+       +---------------+
              |                       |
              -------------------------
                         |
                         v
                    Target Group


---

## Key AWS Services

### Amazon EC2
Elastic Compute Cloud (EC2) provides scalable virtual servers that host applications.

### Elastic Load Balancer (ELB)
ELB distributes incoming traffic across multiple targets to ensure availability and fault tolerance.

---

## Types of Load Balancers

- **Application Load Balancer (ALB)** → HTTP/HTTPS (Layer 7)
- **Network Load Balancer (NLB)** → TCP/UDP (Layer 4)
- **Classic Load Balancer (CLB)** → Legacy

---

## Network Load Balancer (NLB)

- Operates at **Layer 4 (Transport Layer)**
- Handles **millions of concurrent connections**
- Uses **flow hash algorithm** (IP + Port)
- Ultra-low latency
- High throughput

---

## Why NLB Matters

- High-performance applications
- Real-time systems (gaming, trading, streaming)
- Microservices running on different ports
- Scalable backend architectures

---

## Lab Implementation

### Step 1 — Create VPC
- Create custom VPC
- Define CIDR block

---

### Step 2 — Create Subnets
- Create **2 public subnets (different AZs)**

---

### Step 3 — Launch EC2 Instances
- Launch 2 EC2 instances
- Install web server:
sudo yum install httpd -y
sudo systemctl start httpd


---

### Step 4 — Create Target Group
- Protocol: TCP
- Port: 80
- Register EC2 instances

---

### Step 5 — Create Network Load Balancer
- Type: Network Load Balancer
- Scheme: Internet-facing
- Listener: TCP (Port 80)
- Attach target group

---

### Step 6 — Configure Health Checks
- Protocol: TCP
- Ensure instances are healthy

---

### Step 7 — Testing

- Access NLB DNS name
- Refresh multiple times → traffic distributes across instances

---

## Security Insight

NLB operates at Layer 4, meaning:

- No inspection of HTTP headers or content
- Faster but less granular control

Security best practices:

- Use **Security Groups + NACLs**
- Combine with **AWS WAF (via ALB if needed)**
- Monitor with **CloudWatch logs**

---

## Real-World Use Cases

- High-frequency trading systems
- Gaming backends
- IoT platforms
- Microservices architectures
- API gateways requiring low latency

---

## Key Takeaways

- NLB provides ultra-fast traffic distribution
- Operates at transport layer (TCP/UDP)
- Ideal for performance-critical applications
- Complements ALB in layered architectures

