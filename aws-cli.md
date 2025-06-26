 
**AWS CLI Access Keys**
**AWS CLI Setup (Windows)**  
**AWS CLI Hands-on**  
**AWS CloudShell + Region Availability**  
**SDKs (brief mention)**

---

(Day 8)

## Accessing AWS
You have 3 options to access AWS:
- **AWS Management Console** – the web interface I've been interacting with. It is protected by password + perhaps MFA.
- **AWS Command Line Interface (CLI)** – protected by access keys. Access keys are credentials that allow access to AWS via terminal.
- **AWS Software Development Kit (SDK)** – used when you want to call APIs from AWS from within your code. They are protected by access keys.

#### How do we get access keys?
- They can be generated through the AWS Console.
- Users manage their own access keys.
- Access keys from the user's perspective are secret, just like a password. They are not to be shared.
- Treat your **Access Key ID** like a username.  
- Treat your **Secret Access Key** like a password.

---

## What is AWS CLI
- A tool that enables you to interact with AWS services using commands in your command-line shell.
- With this CLI, you get direct access to the public APIs of AWS services.
- Using CLI, you can develop scripts to manage your resources and automate some of your tasks.
- The CLI is open-source and can be found on GitHub.
- This CLI is an alternative to using the AWS Management Console (some users just use CLI).

---

## What is AWS SDK
- **AWS Software Development Kit (AWS SDK)**
- Language-specific APIs
- Allows you to access and manage AWS services programmatically.
- Your SDK is not something you use within your terminal; instead, it's something you embed within your app that *you have to code*.
  - **Example**: your app will contain your SDK that you then use.
- **Supports**:
  - Many different programming languages such as JavaScript, Python, PHP, etc.
  - Mobile SDKs (Android, iOS, ...)
  - Internet of Things (IoT) SDKs (Embedded C, Arduino) in case you're using thermal sensors or backlogs
- **What can you build with AWS SDK?**  
  Prime example: the AWS CLI, which was built with the AWS SDK for Python (named **Boto**).
