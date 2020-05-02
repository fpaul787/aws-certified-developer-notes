# IAM: Identity and Access Management

#### AWS Regions and Availability Zones:
AWS has many different data centers and facilities in multiple regions in the world. Each region has its own, separate copies of AWS services. To use these services you must specify which region you using to process the request. 

The data centers located in each AWS region are grouped in Availability Zones. Regions can have multiple Availability Zones (AZ). Having multiple AZs in a region makes the AWS services highly available. 

#### IAM:

When you first create an AWS account you will have a root account. When accessing AWS, the root account should **never** be used. The root must never be shared as well. 

Permissions can be created for different functions. 
- Users: A physical person
- Groups: Functions (admin, devops) Teams (engineering, design) which contain a group of users
- Roles: Internal usage within AWS resources
- Policies (JSON documents): Defines what each of the above can and cannot do. **Note**: IAM has predefined managed policies.


#### For big enterprises:
- IAM Federation: Integrate their own repository of users with IAM using SAML standard (Active Directory)

#### Policies
IAM policies define permissions for an action regardless of the method that you use to perform the operation.

#### Policy types
- Identity-based policies
  - Attach managed and inline policies to IAM identities (users, groups to which users belong, or roles). Identity-based policies grant permissions to an identity.

- Resource-based policies
  - Attach inline policies to resources. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies. Resource-based policies grant permissions to a principal entity that is specified in the policy. Principals can be in the same account as the resource or in other accounts.

- Permissions boundaries
  - Use a managed policy as the permissions boundary for an IAM entity (user or role). That policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions. Permissions boundaries do not define the maximum permissions that a resource-based policy can grant to an entity.

- Organizations SCPs
  - Use an AWS Organizations service control policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.

- Access control lists (ACLs)
  - Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure. 

- Session policies
  - Pass advanced session policies when you use the AWS CLI or AWS API to assume a role or a federated user. Session policies limit the permissions that the role or user's identity-based policies grant to the session. 

#### AWS Policy Simulator
- When creating new custom policies you can test using:
  - https://policysim.aws.amazon.com/home/index.jsp
  - This policy tool can you save you time in case your custom policy statement's permission is denied
- Alternatively, you can also use the CLI:
    - Some AWS CLI commands (not all) contain `--dry-run` option to simulate API calls. This can be used to test permissions.
    - If the command is successful, you'll get the message: `Request would have succeeded, but DryRun flag is set`
    - Otherwise, you'll be getting the message: `An error occurred (UnauthorizedOperation) when calling the {policy_name} operation`
  
#### Key Points:
- **ONE** IAM User per person 
- One IAM Role per Application
- IAM credentials should **NEVER** be shared
- **NEVER** write IAM credentials in your code. 
- Never use the ROOT account except for initial setup
- It's best to give users the minimal amount of permissions to perform their job