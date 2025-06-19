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
