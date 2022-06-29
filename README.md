<div align="center" id="top"> 
  <img src="img/workflow.png" alt="Splunk_DataManager" />

  &#xa0;

  <!-- <a href="https://splunk_datamanager.netlify.app">Demo</a> -->
</div>

<h1 align="center">Splunk_DataManager</h1>

<p align="center">
  <img alt="Github top language" src="https://img.shields.io/github/languages/top/stax-el-gato/splunk_datamanager?color=56BEB8">

  <img alt="Github language count" src="https://img.shields.io/github/languages/count/stax-el-gato/splunk_datamanager?color=56BEB8">

  <img alt="Repository size" src="https://img.shields.io/github/repo-size/stax-el-gato/splunk_datamanager?color=56BEB8">

  <!-- <img alt="License" src="https://img.shields.io/github/license/stax-el-gato/splunk_datamanager?color=56BEB8">

  <img alt="Github issues" src="https://img.shields.io/github/issues/stax-el-gato/splunk_datamanager?color=56BEB8">

  <img alt="Github forks" src="https://img.shields.io/github/forks/stax-el-gato/splunk_datamanager?color=56BEB8"> -->

  <img alt="Github stars" src="https://img.shields.io/github/stars/stax-el-gato/splunk_datamanager?color=56BEB8">
</p>

<!-- Status -->

<!-- <h4 align="center"> 
	🚧  Splunk_DataManager 🚀 Under construction...  🚧
</h4> 

<hr> -->

<p align="center">
  <a href="#dart-about">About</a> &#xa0; | &#xa0; 
  <a href="#sparkles-features">Features</a> &#xa0; | &#xa0;
  <a href="#rocket-technologies">Technologies</a> &#xa0; | &#xa0;
  <a href="#white_check_mark-requirements">Requirements</a> &#xa0; | &#xa0;
  <a href="#checkered_flag-starting">Starting</a> &#xa0; | &#xa0;
  <a href="#memo-license">License</a> &#xa0; | &#xa0;
  <a href="https://github.com/stax-el-gato" target="_blank">Author</a>
</p>

<br>

## :dart: About ##

## Choose a Control Account ##
The AWS admin must choose an existing control account / new control account for this data input. The control account is an AWS account where you will drive StackSet operations. It allows you to create, update, and delete StackSets to manage resources across multiple data accounts and regions.

## Create the AWSCloudFormationStackSetAdministrationRole in the Control Account ## 
If this role already exists in the control account, the AWS admin can skip this step. If the role doesn’t exist, then the AWS admin creates the AWSCloudFormationStackSetAdministrationRole in the control account. This role allows you to manage StackSet operations from the control account. Learn more

[View Role Policy](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/AWSCloudFormationStackSetAdministrationRole.json)


[View Trust Relationship](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/AWSCloudFormationStackSetAdministrationRole.TrustedRelationship.json)


## Create the SplunkDMReadOnly Role in the Control Account ## 
If this role already exists in the control account, the AWS admin can skip this step. If the role doesn’t exist, then the AWS admin creates the SplunkDMReadOnly role in the control account. This role is needed in the control account for reading IAM user and CloudFormation StackSet status. Make sure that the AWS administrator replaces the account identifiers in the policy. Learn more

[View Role Policy](https://github.com/stax-el-gato/splunk_DataManager/blob/main/SplunkDMReadOnly.Rolepolicy.json)

[View Trust Relationship](https://github.com/stax-el-gato/splunk_DataManager/blob/main/SplunkDMReadOnly.Rolepolicy.TrustedRelationship.json)
 

## (Optional) Create the Onboarding User in the Control Account ## 
If you are the AWS admin and will be completing the AWS data onboarding, then you can use your admin privileges to complete the next steps. If you want a different user to continue with the onboarding, then create a user in the AWS account with the following permissions. The user can be created as an IAM user, IAM role, SAML user, or any of your company’s AWS user creation policies. Make sure that this user has both AWS CLI and console access. Make sure that the AWS administrator replaces the account identifiers in the policy.

[View Permissions](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/Permissions.json)


## Create the AWSCloudFormationStackSetExecutionRole in Data Accounts ## 
If this role already exists in each data account that you’ll be using for this data input, the AWS admin can skip this step. If the role doesn’t exist, then the AWS admin creates the AWSCloudFormationStackSetExecutionRole in each data account. This role allows the control account to create stack instances in your data accounts. The stack instances create resources that include AWS IAM roles, Amazon CloudWatch log subscription filters, Amazon EventBridge rules, and Amazon Kinesis Data Firehose delivery streams. Make sure that the AWS administrator replaces the account identifiers in the trust relationship. Learn more

[View Role Policy](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/AWSCloudFormationStackSetExecutionRole.json)

[View Trust Relationship](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/AWSCloudFormationStackSetExecutionRole.TrustedRelationship.json)


## Create the SplunkDMReadOnly Role in the Data Accounts ##
Download the CloudFormation Template that you will use in your control account to create a StackSet that will create this role in each data account. Select only one region for deployment, preferably us-east-1, because that is where the AWS IAM roles are created. Do not deploy this template in more than one region. This role allows Splunk Cloud to read data from selected AWS services.  Learn more


[AWS CloudFormation Template](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/splunkdm-multi-data-account-readonly-role-template.json)

[View Role Policy](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/SplunkDMReadOnly.Rolepolicy.json)

[View Trust Relationship](https://github.com/stax-el-gato/splunk_DataManager/blob/CMD-1489-splunk-addon-data-manager/Control_tower/SplunkDMReadOnly.Rolepolicy.TrustedRelationship.json)


## Prepare Data Sources for Ingestion ## 
If you use AWS CloudTrail as a data source, make sure that your CloudTrail is configured to send its data to a Amazon CloudWatch log group for the accounts and regions that you select. See Sending Events to Amazon CloudWatch Logs

If you use AWS Security Hub or Amazon GuardDuty, make sure that your Security Hub or GuardDuty is enabled for the accounts and regions that you select. See Enabling AWS Security Hub and Enabling Amazon GuardDuty

If you use AWS Identity and Access Management (IAM) Access Analyzer, make sure that your AWS Identity and Access Management (IAM) Access Analyzer is enabled for the accounts and regions that you select. See Enabling AWS Identity and Access Management (IAM) Access Analyzer
## :sparkles: Features ##
(Coming soon)
:heavy_check_mark: Feature 1;\
:heavy_check_mark: Feature 2;\
:heavy_check_mark: Feature 3;



Made with :heart: by <a href="https://github.com/stax-el-gato" target="_blank">YouMustCallMeKnightHawk</a>

&#xa0;

<a href="#top">Back to top</a>
