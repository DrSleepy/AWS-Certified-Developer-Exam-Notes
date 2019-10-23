# IAM - Identity Access Management

Manage users and their level of access. It is NOT limited by regions

## IAM - What does IAM give you?

1. Is the center of control for your AWS account
2. Allows Shared access to your AWS account
3. Allows Granular permissions -
   1. Give users tailored permissions
4. Allows Identity Federation Management (IFM) -
   1. Allows users to be authenticated using 3rd Party services such as Facebook
5. Allows multifactor authentication
6. Allows users/devices to obtain temporary access to your AWS resources (such as S3) -
   1. Still requires a password
7. Allow you to set up a password rotation policy
8. Supports PCI DSS Compliance -
   1. It must be PCI DSS Compliant in order to meet industry standards for payments
9. Cross-Account access gives you the ability to manager resources in another AWS account

## IAM - Critial Terms

1. Users - such as a developer
2. Groups - such as HR, admins, developers etc. a collections of users under 1 or more permissions
3. Roles - assigned to other root AWS accounts or more commonly assigned AWS services such as Lambda functions to be able to access S3
4. Policies - a policy is a single rule defining what permissions it gives. Can be attatched to a user, group or role

## IAM - 5 Recommended Secruity Steps

1. Delete your root access keys
2. Activate MFA on your root account
3. Create individual IAM users
4. User groups to assign permissions
5. Apply an IAM password policy

## Types of Policies

**Managed Policy:**

- A policy created and managed by AWS (i.e FullAdminAccess)
- Cannot be changed

**Custom Policy:**

- A custom policy you create and manage
- Can be changed

**Inline Policy:**

- A policy that is ONLY used on one user, group or role
- Cannot be attached to multiple users, groups or roles
- When the user, group or role with the policy is deleted, the policy is also deleted

## Assume Role With Web Identity

- Assume Role With Web Identity is an API provided by Security Token Service (STS)
- Returns temporary security credentials for users authenticated by a mobile or web application using a Web ID Provider like Facebook
- For mobile applications, Cognito is recommended
- Regular web applications can use the STS assume-role-with-web-identity API
- Under the hood, assume-role-with-web-identity API calls are made using Cognito
- assume-role-with-web-identity flow:
  1. Client logs in using Facebook
  2. Facebook return JWT to client
  3. Client calls assume-role-with-web-identity API
  4. assume-role-with-web-identity API uses STS to return temporary credentials
  5. Client can now use temporary credentials to access AWS resources (temporary credentials last 1 hour by default)
- AssumedRoleUser ARN and AssumedRoleID are used to programatically reference the temporary credentials. These are not related to an IAM role or user


## Testing IAM Policies

- Use the IAM Policy Simulator

