Prerequisites for Onboarding Data from Multiple Accounts
Ask your AWS admin to prepare the policies and onboarding roles that you need for the next steps.
1. Choose a Control Account
The AWS admin must choose an existing control account / new control account for this data input. The control account is an AWS account where you will drive StackSet operations. It allows you to create, update, and delete StackSets to manage resources across multiple data accounts and regions.

2. Create the AWSCloudFormationStackSetAdministrationRole in the Control Account
If this role already exists in the control account, the AWS admin can skip this step. If the role doesn’t exist, then the AWS admin creates the AWSCloudFormationStackSetAdministrationRole in the control account. This role allows you to manage StackSet operations from the control account. Learn more

View Role Policy
View Trust Relationship
3. Create the SplunkDMReadOnly Role in the Control Account
If this role already exists in the control account, the AWS admin can skip this step. If the role doesn’t exist, then the AWS admin creates the SplunkDMReadOnly role in the control account. This role is needed in the control account for reading IAM user and CloudFormation StackSet status. Make sure that the AWS administrator replaces the account identifiers in the policy. Learn more

View Role Policy
View Trust Relationship
4. (Optional) Create the Onboarding User in the Control Account
If you are the AWS admin and will be completing the AWS data onboarding, then you can use your admin privileges to complete the next steps. If you want a different user to continue with the onboarding, then create a user in the AWS account with the following permissions. The user can be created as an IAM user, IAM role, SAML user, or any of your company’s AWS user creation policies. Make sure that this user has both AWS CLI and console access. Make sure that the AWS administrator replaces the account identifiers in the policy.

View Permissions
5. Create the AWSCloudFormationStackSetExecutionRole in Data Accounts
If this role already exists in each data account that you’ll be using for this data input, the AWS admin can skip this step. If the role doesn’t exist, then the AWS admin creates the AWSCloudFormationStackSetExecutionRole in each data account. This role allows the control account to create stack instances in your data accounts. The stack instances create resources that include AWS IAM roles, Amazon CloudWatch log subscription filters, Amazon EventBridge rules, and Amazon Kinesis Data Firehose delivery streams. Make sure that the AWS administrator replaces the account identifiers in the trust relationship. Learn more

View Role Policy
View Trust Relationship
6. Create the SplunkDMReadOnly Role in the Data Accounts
Download the CloudFormation Template that you will use in your control account to create a StackSet that will create this role in each data account. Select only one region for deployment, preferably us-east-1, because that is where the AWS IAM roles are created. Do not deploy this template in more than one region. This role allows Splunk Cloud to read data from selected AWS services.  Learn more


AWS CloudFormation Template
View Role Policy
View Trust Relationship
7. Prepare Data Sources for Ingestion
If you use AWS CloudTrail as a data source, make sure that your CloudTrail is configured to send its data to a Amazon CloudWatch log group for the accounts and regions that you select. See Sending Events to Amazon CloudWatch Logs

If you use AWS Security Hub or Amazon GuardDuty, make sure that your Security Hub or GuardDuty is enabled for the accounts and regions that you select. See Enabling AWS Security Hub and Enabling Amazon GuardDuty

If you use AWS Identity and Access Management (IAM) Access Analyzer, make sure that your AWS Identity and Access Management (IAM) Access Analyzer is enabled for the accounts and regions that you select. See Enabling AWS Identity and Access Management (IAM) Access Analyzer