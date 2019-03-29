# IAM - Identity Access Management

Manage users and their level of access. It is NOT limited by regions

## IAM - What does IAM give you?

1. Is the center of control for your AWS account
2. Allows Shared access to your AWS account
3. Allows Granular permissions -
   3.1 Give users tailored permissions
4. Allows Identity Federation Management (FIM) -
   4.1 Allows users to be authenticated using 3rd Party services such as Facebook
5. Allows multifactor authentication
6. Allows users/devices to obtain temporary access to your AWS resources (such as S3) -
   6.1 Still requires a password
7. Allow you to set up a password rotation policy
8. Supports PCI DSS Compliance -
   8.1 It must be PCI DSS Compliant in order to meet industry standards for payments

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
