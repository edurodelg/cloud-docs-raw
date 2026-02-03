---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/work-with-ami-store-restore.html
fetched_at: 2026-02-04T00:11:28.538655
---

# Create a store image task

When you store an AMI in an S3 bucket, a store image task is created. You can use the store image task to monitor the progress and outcome of the process.

###### Contents

## Securing your AMIs

It is important to ensure that the S3 bucket is configured with sufficient security to
secure the content of the AMI and that the security is maintained for as long as the AMI
objects remain in the bucket. If this can't be done, use of these APIs is not
recommended. Ensure that public access to the S3 bucket is not allowed. We recommend
enabling [Server-side encryption](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html)
for the S3 buckets in which you store the AMIs, although it’s not required.

For information about how to set the appropriate security settings for your S3 buckets, review the following security topics:

When the AMI snapshots are copied to the S3 object, the data is then copied over TLS connections. You can store AMIs with encrypted snapshots, but the snapshots are decrypted as part of the store process.

## Permissions for storing and restoring AMIs using S3

If your IAM principals will store or restore AMIs using Amazon S3, you need to grant them the required permissions.

The following example policy includes all of the actions that are required to allow an IAM principal to carry out the store and restore tasks.

You can also create IAM policies that grant principals access to specific resources only.
For more example policies, see [
Access management for AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) in the *IAM User Guide*.

###### Note

If the snapshots that make up the AMI are encrypted, or if your account is enabled for encryption by default, your IAM principal must have permission to use the KMS key.

## Create a store image task

To store an AMI in an S3 bucket, start by creating a store image task. The time it takes to complete the task depends on the size of the AMI. You can track the progress of the task until it either succeeds or fails.

## Create a restore image task

You must specify a name for the restored AMI. The name must be unique for AMIs in the Region for this account. The restored AMI gets a new AMI ID.