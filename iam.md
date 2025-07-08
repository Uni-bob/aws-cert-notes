# Identity and Access Management

## IAM Users & Groups
- IAM is a global service.
- A root account is created by default, which is what happened when I created my AWS account. After account creation, it's best practice to not use or share the root account.
- Instead, create users — individuals within your organization that you can assign to groups.
- Groups only contain users, not other groups.
- Users do not have to belong to a group, although it's against best practice. Users can belong to multiple groups.

> **Example:** You can have Alice, Bob, and Charles assigned to a group named `Developers`, and David and Edward assigned to a group named `Operations`. If there is a third group named `Audit Team`, you can assign Charles and David to that group even though they are already assigned to another group.

## Permissions
- We create users and groups for the purpose of assigning them specific permissions.
- Users or groups can be assigned JSON documents called **policies**.
- These policies define the permissions of users for any given service within AWS.
- For the sake of security and to avoid unnecessary risk in AWS, apply the **principle of least privilege**: Don’t give more permissions than a user needs — kind of like “need to know” in the military.
- One way to manage permissions for users is to create a group and assign that group a permission then by adding a given user to that group, the user inherits any permissions assigned to that group.

(Day 6)
## IAM Policy Structure

- Important to get **familiar** with this structure as you will see **a lot** of it in AWS.
- Policy is in a `.JSON` file.
- Consists of:
  - **Version**: Has a policy version number or policy language version (always include `'2012-10-17'`).
  - **ID**: An identifier for the policy (optional).
  - **Statements**: Can have one or more individual statements (required).

- Statements consist of:
  - **Sid**: Or statement ID, is an identifier for the statement (optional).
  - **Effect**: The effect of the policy itself — whether the statement allows or denies access (`Allow`, `Deny`).
  - **Principal**: Deals with which account, user, or role this policy is applied to.
  - **Action**: The list of actions this policy allows or denies (based on the `"Effect"` on file).
  - **Resource**: List of resources to which the actions are applied.
  - **Condition**: (Not seen in example) The condition for when this policy is in effect or is not (optional).

- Going into the exam, make sure to be familiar with what a policy consists of: Version, ID, Statements — Sid, Effect, Principal, Action, Resource.

> **Example**
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "elasticloadbalancing:Describe*",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudwatch:ListMetrics",
        "cloudwatch:GetMetricStatistics",
        "cloudwatch:Describe*"
      ],
      "Resource": "*"
    }
  ]
}
```

## IAM Security

- To protect users and groups we have 2 defense mechanisms:
    - **Password Policy**: strong passwords = higher security for account.
    - In AWS you can set up a password policy and define parameters for the password such as:
        - Set a minimum password length
        - Require specific character types:
            - uppercase letters
            - lowercase letters
            - numbers
            - non-alphanumeric characters
        - User being allowed to change their own passwords
        - Require users to change their password after some time (password expiration)  
        **Example:** "Every 90 days users must change their passwords".
        - Prevent password re-use
    - **Multi-Factor Authentication - MFA**
        - Because of the power one has on a root account or a user with admin privileges, we want to take the extra security step and use MFA.
        - He states that you absolutely, at least, want to protect your Root Accounts & hopefully your IAM users.
        - This is achieved through the use of an MFA device. MFA = a password you know + security device you own.
        - **Main Benefit of MFA**: if a user's pass is stolen or hacked, the system will not be compromised because the hacker will also need the physical device that the given user owns and has their MFA token on.
        - AWS MFA device options (Exam Important):
            - Virtual MFA device, such as Google Authenticator, which is what I'm used to.
                - Support for multiple tokens on a single device.
            - Universal 2nd Factor (U2F) Security Key
                - This is a physical device.
                - For ex: YubiKey by Yubico. Looks like a flash drive.
                - Support for multiple root and IAM users using a single security key so you don't need as many keys as users. (Because that could get hectic real fast).
            - Hardware Key Fob MFA Device
            - Hardware Key Fob MFA Device for AWS GovCloud (US). Special key fob.

(Day 10)
## IAM Roles for Services
- AWS services that launch will need to perform actions on our behalf. To make this possible we need to assign AWS services permissions to do so, just like with users. To achieve this, we use what is known as an "IAM Role".
- These IAM Roles will function like a user but are intended for an AWS service rather than a physical user.  
**Ex**: An IAM Role for an "EC2 Instance" which is a virtual server wants to access a service from AWS. As long as we've assigned that IAM Role the appropriate permission, it will gain access and allow the action or call to a particular API or what have you.
- Common roles:
  - EC2 Instance roles
  - Lambda function roles
  - Roles for CloudFormation

(Day 11)  
(iam roles hands-on)

- You have 5 different roles you can create atm; for exam purposes focus on "AWS service" identity type.

## IAM Security Tools
- **IAM Credentials Report**:
  - This is done at the (root) account level and is a report that lists all your account users and the status of their various credentials.

- **IAM Access Advisor**:
  - This is done at the user level. The access advisor shows the service permissions granted to a user and when those services were last accessed.  
  **Note**: In 2025, where the "Access Advisor" tab would be on a user page, it is now replaced with "Last Accessed".

- These tools are helpful when it comes to implementing the **principle of least privilege**.
- Through the reports we will be able to see what permissions have not been accessed at all or accessed barely and remove unneeded permissions accordingly.

## IAM General Guidelines & Best Practices
- Don't use the root account except for AWS account setup.
- One physical user should equal one AWS user. Meaning if someone else needs to use AWS, create a user for them—don't lend them yours.
- **Assign users to groups** and assign permissions to groups.
- Create a strong password policy.
- If possible, use and enforce strict use of MFA.
- Create and use Roles for giving permissions to AWS services.
- Use Access Keys for Programmatic Access (CLI/SDK).
- Audit permissions of your account using IAM Credentials Report & IAM Access Advisor (Last Accessed tab).
- Never share IAM users & Access Keys.

## IAM Section - Summary
- Users: mapped to a physical user, has a password for AWS Console.
- Groups: contain users only.
- Policies: JSON document that outlines permissions for users or groups.
- Roles: an entity but for AWS services such as EC2 instances (virtual server).
- Security: MFA + Password Policy.
- AWS CLI: manage AWS services using the command-line.
- AWS SDK: manage AWS services using a programming language.
- Access Keys: access AWS using the CLI or SDK.
- Audit: IAM Credential Reports & IAM Access Advisor (Last Accessed tab).
