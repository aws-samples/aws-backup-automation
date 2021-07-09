# Blog Post - [Automate centralized backup at scale across AWS services using AWS Backup](https://aws.amazon.com/blogs/storage/automate-centralized-backup-at-scale-across-aws-services-using-aws-backup/)

This solution demonstrates how you can save time using AWS CloudFormation automation to centrally automate and scale the process of implementing AWS Backup policies, backup vaults, and cross-Region, cross-account replication across your multi-account AWS environment. Using this solution, you can easily manage AWS Backup with automation and implement a data protection strategy that mitigates the risk of data loss.. In this repository, you will find all the AWS CloudFormation templates and Python code that will build this solution in your AWS environment. 


## Solution architecture and design
The following diagram illustrates the AWS Backup automation solution discussed in this blog and repository:

## ![](/Images/aws-backup-automation.jpg)

The workflow and architecture of the solution works as follows:

In the management account (the environment hosting your AWS Organizations):

1. Opt in to use the AWS Backup service and cross-account management features. See the blog post on how to [Automate centralized backup at scale across AWS services using AWS Backup](https://aws.amazon.com/blogs/storage/automate-centralized-backup-at-scale-across-aws-services-using-aws-backup/) for further details.
2. [aws-backup-member-account.yaml](./CloudFormation/aws-backup-member-account.yaml): This stackset implements the local backup vaults, IAM roles, and vault AWS KMS encryption keys in member accounts 1 and 2. We assume that the supported AWS Backup resources in the member accounts are tagged as indicated in the prerequisites section of the blog. The stackset should be deployed to the member accounts.
3. [aws-backup-central-backup-account.yaml](./CloudFormation/aws-backup-central-backup-account.yaml): This stackset implements the central backup vault, IAM role, vault AWS KMS encryption key, and vault access policy in the backup account. The stackset should be deployed to the central backup account.
4. [aws-backup-org-policy.yaml](./CloudFormation/aws-backup-org-policy.yaml): This stack implements a Lambda function, Lambda IAM role, and centralized backup policies. The backup policies consist of tag-based and cross-account, cross-Region copy policies that are automatically attached to the root OU and inherited by all AWS Organizations accounts. The stackset should be deployed to the management account.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

