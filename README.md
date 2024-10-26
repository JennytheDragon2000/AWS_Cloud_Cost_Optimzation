# EBS Snapshot Cleanup Lambda Function

This AWS Lambda function automates the cleanup of unused Elastic Block Store (EBS) snapshots in your AWS account. It identifies and deletes snapshots that are no longer attached to active EC2 instances or associated with any EBS volume. 

## Project Overview

EBS snapshots are backups of EBS volumes and can accumulate over time, leading to unnecessary storage costs. This Lambda function performs the following actions:

1. Retrieves all EBS snapshots owned by the AWS account.
2. Identifies all active EC2 instances in the account.
3. Checks each snapshot to determine if it is attached to an EBS volume associated with a running EC2 instance.
4. Deletes snapshots that:
   - Are not attached to any volume.
   - Are taken from volumes that are not attached to running instances.
   - Are associated with volumes that have been deleted.

## Prerequisites

- **AWS Lambda**: Deploy this code as an AWS Lambda function.
- **IAM Permissions**: Ensure the Lambda execution role has the following permissions:
  - `ec2:DescribeSnapshots`
  - `ec2:DescribeInstances`
  - `ec2:DescribeVolumes`
  - `ec2:DeleteSnapshot`

## How to Use

1. **Deploy the Lambda function**:
   - Create a Lambda function in the AWS Console or using the AWS CLI.
   - Copy the code from `lambda_function.py` (this file) into the Lambda function.

2. **Set Up Lambda Execution Role**:
   - Attach an IAM role with the required permissions (listed in Prerequisites) to the Lambda function.

3. **Schedule the Lambda Function (Optional)**:
   - For periodic execution, use Amazon CloudWatch Events to schedule the function (e.g., daily or weekly).
