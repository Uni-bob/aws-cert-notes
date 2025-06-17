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
