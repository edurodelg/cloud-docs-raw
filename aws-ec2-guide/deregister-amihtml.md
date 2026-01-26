---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/deregister-ami.html
fetched_at: 2026-01-26T22:59:05.464655
---

# Deregister an Amazon EC2 AMI

When you deregister an AMI, Amazon EC2 permanently deletes it. After you deregister an AMI, you can't use it to launch new instances. You might consider deregistering an AMI when you have finished using it.

To protect against accidental or malicious deregistering of an AMI, you can turn on [deregistration protection](./ami-deregistration-protection.html). If you accidentally
deregister an EBS-backed AMI, you can use the [Recycle Bin](https://docs.aws.amazon.com/ebs/latest/userguide/recycle-bin.html) to restore it only if you
restore it within the allowed time period before it is permanently deleted.

When deregistering an AMI, you can optionally delete its associated snapshots at the same time. However, if a snapshot is associated with multiple AMIs, it won't be deleted even if specified for deletion, although the AMI will still be deregistered. Any snapshots not deleted will continue to incur storage costs.

Deregistering an AMI has no effect on any instances that were launched from the AMI. You can
continue to use these instances. By default, deregistering an AMI also has no effect on any
snapshots that were created during the AMI creation process. You'll continue to incur usage
costs for these instances and storage costs for the snapshots. Therefore, to avoid incurring
unnecessary costs, we recommend that you terminate any instances and delete any snapshots that
you do not need. You can delete the snapshots either automatically during deregistration or
manually after deregistration. For more information, see [Avoid costs from unused
resources](#delete-unneeded-resources-to-avoid-unnecessary-costs).

For instances launched from an AMI that is subsequently deregistered, you can still view
some high-level information about the AMI by using the
`describe-instance-image-metadata`

AWS CLI command. For more information, see [describe-instance-image-metadata](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-instance-image-metadata.html).

###### Contents

## Considerations

-
You can't deregister an AMI that is not owned by your account.

-
You can't use Amazon EC2 to deregister an AMI that is managed by the AWS Backup service. Instead, use AWS Backup to delete the corresponding recovery points in the backup vault. For more information, see

[Deleting backups](https://docs.aws.amazon.com/aws-backup/latest/devguide/deleting-backups.html)in the*AWS Backup Developer Guide*.

## Deregister an AMI

You can deregister EBS-backed AMIs and Amazon S3-backed AMIs. For EBS-backed AMIs, you can optionally delete the associated snapshots at the same time. However, if a snapshot is associated with other AMIs, it will not be deleted even if specified for deletion.

## Avoid costs from unused resources

Deregistering an AMI doesn't, by default, delete all of the resources that are associated with the AMI. These resources include the snapshots for EBS-backed AMIs and the files in Amazon S3 for Amazon S3-backed AMIs. When you deregister an AMI, you also don't terminate or stop any instances launched from the AMI.

You will continue to incur costs for storing the snapshots and files, and you will incur costs for any running instances.

To avoid incurring these types of unnecessary costs, we recommend deleting any resources that you don't need.

###### EBS-backed AMIs

-
Delete the associated snapshots while deregistering the AMI. For more information, see

[Deregister an AMI](#deregister-an-ami). -
If you deregister an AMI without deleting its associated snaphots, you can manually

[delete the snapshots](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-deleting-snapshot.html#ebs-delete-snapshot). The snapshot of the instance root volume created during AMI creation has the following description format:`Created by CreateImage(`

`i-1234567890abcdef0`

) for`ami-0abcdef1234567890`

-
If you no longer need the instances that were launched from the AMI, you can

[stop](./Stop_Start.html#starting-stopping-instances)or[terminate](./terminating-instances.html#terminating-instances-console)them. To list the instances, filter by the ID of the AMI.

###### Amazon S3-backed AMIs

-
Delete the bundle in Amazon S3 by using the

[ec2-delete-bundle](./ami-tools-commands.html#ami-delete-bundle)(AMI tools) command. -
If the Amazon S3 bucket is empty after you delete the bundle, and you have no further use for that bucket, you can

[delete the bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html). -
If you no longer need the instances that were launched from the AMI, you can

[terminate](./terminating-instances.html#terminating-instances-console)them. To list the instances, filter by the ID of the AMI.