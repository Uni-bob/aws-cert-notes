(Day 12)

## Amazon EC2 Basics

- EC2 is one of the most popular AWS services that they offer.
- EC2 stands for Elastic Compute Cloud, which = Infrastructure as a Service.
- EC2 is not just one service; it's composed of many.
- Mainly consists of the capability to:
  - Rent virtual machines (called EC2 instances)  
  - Store data on virtual drives (EBS volumes)  
  - Distribute load across machines (ELB – Elastic Load Balancer)  
  - Scale services using an auto-scaling group (ASG)

- Knowing EC2 is fundamental to understanding how the cloud works.
- The cloud is used to rent compute power on demand — and EC2 does just that.

## EC2 Sizing & Configuration Options

- Linux, Windows, macOS
- Compute power & number of cores (CPU)
- Amount of RAM
- Storage space:
  - Network-attached (EBS & EFS)
  - Hardware (EC2 Instance Store)
- Network card: speed, public IP address
- Firewall rules: Security Group
- Bootstrap script (configured at first launch): EC2 User Data

(Day 13)

## EC2 User Data

- Bootstrapping means launching commands when a machine starts.
- It is possible to bootstrap our instances using an EC2 User Data script.
- That script is only run once at the instance's first start and will never be run again.
- EC2 User Data is used to automate boot tasks such as:
  - Installing updates and software
  - Downloading common files from the internet
  - Anything else you may think of
  - Keep in mind that the more you add to your data script, the longer your boot time will be.
- The EC2 User Data script runs with the root user. Therefore, any command you include will have "sudo" rights.

## (Hands-On) Launching EC2 Instance Running Linux

- When you stop an instance and later turn it on, it’s possible that Amazon may change the public IP address for your instance.
- The private IP will always stay the same.

(Day 14) Notes

## EC2 Instance Types

- There are different EC2 instance types for different use cases.
- Each EC2 instance type has its own group of families. ex: General Purpose --> m8g, m8g.large, m8g.xlarge
- AWS naming convention for EC2 instance types:
  - m5.2xlarge
    - m: instance class
    - 5: generation of the instance (AWS improves them over time. ex: next would be 6)
    - 2xlarge: size within the instance class (it starts with small and then so on)
      - The larger the size the more CPU power, RAM, storage etc.
(For exam perspective what do you need to know)

**General Purpose** - Great for a diversity of workloads such as web servers or code repositories
- Good balance between: compute, memory, and networking
- In this course we use t2.micro which is a General Purpose EC2 instance

**Compute Optimized** - Great for compute-intensive tasks that require high performance processors. EX:
  - Batch processing workloads
  - Media Transcoding
  - High performance web server
  - High performance computing (HPC)
  - Scientific modeling & machine learning
  - Dedicated gaming servers

**Memory Optimized**
- Fast performance for workloads that process large data sets in memory
- Use case:
  - High performance, relational/non-relational databases
  - Distributed web scale cache stores
  - In-memory databases optimized for BI (business intelligence)
  - Applications performing real-time processing of big unstructured data

**Storage Optimized**
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- Use cases:
  - High frequency online transaction processing (OLTP) systems
  - Relational & NoSQL databases
  - Cache for in-memory databases (for example, Redis)
  - Data warehousing applications
  - Distributed file systems

## Day 15 Notes

### Intro to Security Groups
- Security Groups are fundamental to network security on AWS.
- They control how traffic is allowed into or out of our EC2 Instance.
- Sec Groups only contain 'allow' rules (JSON).
- Sec group rules can reference by IP (where traffic is coming to or from) or by another Sec Group (Sec groups can reference each other).

#### Deeper Dive
- Sec Groups are acting as a "firewall" on an EC2 instance.
- They regulate:
  - Access to ports
  - Oversee authorized IP ranges - IPv4 and IPv6
  - Control of inbound network (from others to the instance)
  - Control of outbound network (from the instance to others)

### Security Groups - Good to Know
- Can be attached to multiple instances (as well as instances can contain multiple Sec Groups).
- Sec groups are locked down to a region/VPC combination (if in another region you'd have to recreate the security group).
- Sec groups live outside of our EC2 — if traffic is blocked the EC2 instance won't even see it (in other words the unwanted traffic never touches our EC2).
- Recommended to maintain one separate Sec Group for SSH access.
- If your app is not accessible (timeout), then it is a Sec Group issue.
- If app gives "connection refused" error, then it is an app error or it has not been launched (in this case the Sec Group did its job and traffic went through, but the app was errored or didn’t launch or something of the sort).
- All inbound traffic is blocked by default.
- All outbound traffic is authorized by default.

#### Exam Important
**Classic Ports to Know**
- 22 = SSH (Secure Shell) - log into a Linux instance
- 21 = FTP (File Transfer Protocol) - upload files into a file share
- 22 = SFTP (Secure File Transfer Protocol) - upload files using SSH
- 80 = HTTP - access unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP (Remote Desktop Protocol) - log into a Windows instance

### SSH Overview
- SSH is a command-line interface utility that can be used on Mac, Linux, and Windows >= 10. You can use PuTTY (uses SSH protocol) for any version of Windows.
- EC2 Instance Connect - uses web browser instead of terminal to connect to EC2 instance. This method is available for all of the platforms above (at the moment only works for Amazon Linux 2).
- SSH is what the majority have trouble with.
- When things don’t work out, rewatch lecture.

---

## Day 16 Notes

### How to SSH into Your EC2 Instance
- SSH is one of the most important functions. It allows you to control a remote machine, all by using the command line.
- Never run `aws configure` on EC2 Instance Connect — you risk someone retrieving the values of your login, exposing your public and private key to anyone else who may have access to that instance.
- Instead, add an IAM role to the instance and it can enable access to commands on your behalf without you having to risk someone else knowing your credentials.

---

## EC2 Instance Purchasing Options
- If you have different kinds of workloads you can optimize discounts and pricing by specifying what you need from AWS.
- **On-demand Instances** - short workload, predictable pricing, pay by second.
- **Reserved (1 & 3 years term)**  
  - Reserved Instance - long workloads  
  - Convertible Reserved Instances - long workloads with flexible instances (if you want to change instance type over time)
- **Savings Plans (1 & 3 years term)** - Instead of committing to a certain instance type, you commit to an amount of usage in dollars; meant for long workloads as well.
- **Spot Instances** - short workloads, cheap, can lose instances (less reliable).
- **Dedicated Hosts** - book an entire physical server, control instance placement.
- **Dedicated Instances** - no other customers will share your hardware.
- **Capacity Reservations** - reserve capacity in a specific AZ for any duration.

---

### EC2 On Demand
- Pay for what you use:
  - Linux or Windows - billing per second, after the first minute
  - All other operating systems - billing per hour
- Has the highest cost but no upfront payment.
- No long-term commitment.
- Recommended for short-term & uninterrupted workloads, where you can't predict how the app will behave.

(Day 17 Notes)

## EC2 Reserved Instances
- Up to 72% discount compared to On-Demand.  
- You reserve specific instance attributes (Instance Type, Region, Tenancy, OS).  
- Specify a reservation period to unlock an even heavier discount (1 to 3 years). The longer, the better the discount.  
- Payment options: No upfront (+), Partial Upfront (++), All Upfront (+++).  
- Reserved Instance Scope: Regional or Zonal (reserve capacity in an AZ).  
- You’d use Reserved Instances for steady-state, low-volatility apps (think database).  
- You can buy and sell your Reserved Instances in a marketplace if no longer needed.  

### Convertible Reserved Instance
- Allows you to change the instance type, instance family, OS, scope, and tenancy.  
- Because you have more flexibility, you get a slightly weaker discount (e.g., ~66% compared to 72%).  

---

## EC2 Savings Plans
- Get a discount based on long-term usage.  
- Commit to a certain type of usage (e.g., $10/hr for 1 or 3 years).  
- Any usage beyond the EC2 Savings Plan is billed at the On-Demand price.  
- Locked to a specific instance family & AWS region (e.g., M5 in us-east-1).  
- Flexible across:  
  - Instance Size (e.g., m5.xlarge or m5.2xlarge)  
  - OS (Linux or Windows)  
  - Tenancy (Host, Dedicated, Default)  

---

## EC2 Spot Instances
- Tend to have the heaviest discount.  
- You can lose your instance at any time if your max price is less than the current spot price.  
- Most cost-efficient instances in AWS.  
- Useful for workloads that are resilient to failure:  
  - Batch jobs  
  - Data analysis  
  - Image processing  
  - Any distributed workloads  
  - Workloads with a flexible start and end time  
- **Not suitable for critical jobs or databases** (Exam relevant).  

---

## EC2 Dedicated Hosts
- A physical server with EC2 instance capacity fully dedicated to your use.  
- Allows you to address **compliance requirements** and use your existing server-bound software licenses (billing per-socket, per-core, per-VM software licenses).  
- Purchasing options:  
  - On-Demand – pay per second for active Dedicated Host.  
  - Reserved – 1 or 3 years (No upfront, Partial Upfront, All Upfront).  
- Most expensive option.  
- Useful for software with complicated licensing models (BYOL – Bring Your Own License).  
- Ideal for companies with strong regulatory or compliance needs.  

---

## Dedicated Instances
- Instances run on hardware that’s dedicated to you.  
- Different from a physical server but may share hardware with other instances on the same account.  
- No control over instance placement (can move hardware after stop/start).  

**Remember (Exam):**  
- **Dedicated Instances** → Your own instance on your own hardware.  
- **Dedicated Host** → Access to the physical server itself, plus visibility into lower-level hardware details (per-socket, per-core, etc.).  
