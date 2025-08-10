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

(Day 15 Notes)

## Intro to Security Groups
- Security Groups are fundamental to network security on AWS  
- They control how traffic is allowed into or out of our EC2 Instance  
- Sec Groups only contain 'allow' rules (JSON)  
- Sec Groups rules can reference by IP (where traffic is coming to or from) or by another Sec Group (Sec Groups can reference each other)  

### Deeper Dive
- Sec Groups are acting as a "firewall" on EC2 instance  
- They regulate:  
  - Access to ports  
  - Oversee Auth IP ranges – IPv4 and IPv6  
  - Control of inbound network (from other to the instance)  
  - Control of outbound network (from the instance to other)  

## Security Groups - Good to Know
- Can be attached to multiple instances (as well as instances can contain multiple Sec Groups)  
- Sec Groups are locked down to a region / VPC combination (if in another region you'd have to recreate the security group)  
- Sec Groups live outside of our EC2 – if traffic is blocked the EC2 instance won't even see it (in other words the unwanted traffic never touches our EC2)  
- Recommends to maintain one separate Sec Group for SSH access  
- If your app is not accessible (timeout), then it is a Sec Group issue  
- If app gives "connection refused" error, then it is an app error or it has not been launched (in this case the Sec Group did its job and traffic went through but the app was errored or didn’t launch or something of the sort)  
- All inbound traffic is blocked by default  
- All outbound traffic is authorized by default  

### Exam Important - Classic Ports to Know
- **22** = SSH (Secure Shell) – log into a Linux instance  
- **21** = FTP (File Transfer Protocol) – upload files into a file share  
- **22** = SFTP (Secure File Transfer Protocol) – upload files using SSH  
- **80** = HTTP – access unsecured websites  
- **443** = HTTPS – access secured websites  
- **3389** = RDP (Remote Desktop Protocol) – log into a Windows instance  

## SSH Overview
- SSH is a command-line interface utility that can be used on Mac, Linux, and Windows >= 10. You can use PuTTY (uses SSH protocol) for any version of Windows.  
- EC2 Instance Connect – uses web browser instead of terminal to connect to EC2 instance. This method is available for all of the platforms above (at the moment only works for Amazon Linux 2)  
- SSH is what the majority have trouble with  
- When things don’t work out, rewatch lecture  
