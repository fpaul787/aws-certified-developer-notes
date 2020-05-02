# IAM: Identity and Access Management

#### AWS Regions and Availability Zones:
AWS has many different data centers and facilities in multiple regions in the world. Each region has its own, separate copies of AWS services. To use these services you must specify which region you using to process the request. 

The data centers located in each AWS region are grouped in Availability Zones. Regions can have multiple Availability Zones (AZ). Having multiple AZs in a region makes the AWS services highly available. 

#### Choosing a Region
There are many factors that go into choosing an AWS Region. The factors include latency, price, and data residency. AWS Region strings end in a number (us-east-1, us-west-2). AZ strings end in number (us-east-1a).

#### IAM:

When you first create an AWS account you will have a root account. When accessing AWS, the root account should **never** be used. The root must never be shared as well. 

Permissions can be created for different functions. 
- Users: A physical person
- Groups: Functions (admin, devops) Teams (engineering, design) which contain a group of users. Example,  all developers working on a specific project could each have their own
IAM user. Each of these users can be added to a group, named developers , to manage their
permissions collectively. 
- Roles: Internal usage within AWS resources. Best used for short term operations.
  - There might be a case where you don't want to create and manage new sets of long-term credientials for team members or applications.

  - Another case would be giving permissions for AWS services to perform actions on your behalf. An example of this is an EC2 making AWS API calls.
  - To control acces to an IAM roles, define a trust policy that specifies which *principals* can assume a role. Principals include AWS services and also users who have been authenticated. 
  - When a principal assumes a role, AWS provides  new short term security credentials that are valid for a time-limited session through the AWS Security Token Service (AWS STS).
    - those credentials are composed of an access Key ID, secret access key, and, additionally, a session token with a known expiration date. 
    
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

#### Custom Policies
You can define custom policies when you need more control. An IAM policy is a JSON-style document composed of one or more statements. Each statement has an effect that will either allow or deny access
to specific API actions on AWS resources. A deny statement takes precedence over any
allow statements. Use an Amazon Resource Name(ARN) to specify precisely the resource or resources to which a custom policy applies. 



#### Amazon Resource Name
An ARN always starts with arn: and can include the following components to identify a
particular AWS resource uniquely:
- **Partition** Usually aws. For some regions, such as in China, this can have a different
value.
- **Service** Namespace of the AWS service.
Region The region in which the resource is located. Some resources do not require a
region to be specified.
- **Account ID** The account in which the resource resides. Some resources do not require an account ID to be specified.
- **Resource** The specific resource within the namespace of the AWS service. For services that
have multiple types of resources, there may also be a resource type.


These are example formats for an ARN:

arn:partition:service:region:account-id:resource
arn:partition:service:region:account-id:resourcetype/resource
arn:partition:service:region:account-id:resourcetype:resource

Examples of ARNs for various AWS resources:
<!-- Amazon Polly Lexicon -->
arn:aws:polly:us-west-2:123456789012:lexicon/awsLexicon
<!-- IAM user name -->
arn:aws:iam::123456789012:user/carla
  
## Key Points:
- **ONE** IAM User per person 
- One IAM Role per Application
- IAM credentials should **NEVER** be shared
- **NEVER** write IAM credentials in your code. 
- Never use the ROOT account except for initial setup
- It's best to give users the minimal amount of permissions to perform their job

## Things you should know
- Ways to manage AWS resources.
  - AWS SDK, AWS CLI, and AWS Management Console are ways to manage AWS resources in your account.
- Importance of AWS Regions
  - Be able to identify the impact of AWS Region selection on your application code. Also know how region selection impacts API calls and API endpoints. 

- Know about IAM users and IAM roles
  - Understand when it is appropriate to use IAM uses or IAM roles for a given applicaiton that needs to make AWS API calls. 

- Know how to recognize valid IAM policies
  - Identify valid IAM policies and predict the effects of policy statements. 