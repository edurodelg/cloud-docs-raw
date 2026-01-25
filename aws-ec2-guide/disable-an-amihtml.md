---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/disable-an-ami.html
fetched_at: 2026-01-25T15:11:45.123896
---

# Disable an Amazon EC2 AMI

You can disable an AMI to prevent it from being used for instance launches. You can't launch new instances from a disabled AMI. You can re-enable a disabled AMI so that it can be used again for instance launches.

You can disable both private and public AMIs.

To reduce storage costs for disabled EBS-backed AMIs that are rarely used, but which need
to be retained long term, you can archive their associated snapshots. For more information,
see [Archive
Amazon EBS snapshots](https://docs.aws.amazon.com/ebs/latest/userguide/snapshot-archive.html) in the *Amazon EBS User Guide*.

###### Contents

## How AMI disable works

###### Warning

Disabling an AMI removes all its launch permissions.

###### When an AMI is disabled:

-
The AMI's state changes to

`disabled`

. -
A disabled AMI can't be shared. If an AMI was public or previously shared, it is made private. If an AMI was shared with an AWS account, organization, or Organizational Unit, they lose access to the disabled AMI.

-
A disabled AMI does not appear in

[DescribeImages](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_DescribeImages.html)API calls by default. -
A disabled AMI does not appear under the

**Owned by me**console filter. To find disabled AMIs, use the**Disabled images**console filter. -
A disabled AMI is not available to select for instance launches in the EC2 console. For example, a disabled AMI does not appear in the AMI catalog in the launch instance wizard or when creating a launch template.

-
Launch services, such as launch templates and Auto Scaling groups, can continue to reference disabled AMIs. Subsequent instance launches from a disabled AMI will fail, so we recommend updating launch templates and Auto Scaling groups to reference available AMIs only.

-
EC2 instances that were previously launched using an AMI that is subsequently disabled are not affected, and can be stopped, started, and rebooted.

-
You can't delete snapshots associated with disabled AMIs. Attempting to delete an associated snapshot results in the

`snapshot is currently in use`

error.

###### When an AMI is re-enabled:

-
The AMI's state changes to

`available`

, and it can be used to launch instances. -
The AMI can be shared.

-
AWS accounts, organizations, and Organizational Units that lost access to the AMI when it was disabled do not regain access automatically, but the AMI can be shared with them again.


## Costs

When you disable an AMI, the AMI is not deleted. If the AMI is an EBS-backed AMI, you
continue to pay for the AMI's EBS snapshots. If you want to keep the AMI, you might be
able to reduce your storage costs by archiving the snapshots. For more information, see
[Archive Amazon EBS snapshots](https://docs.aws.amazon.com/ebs/latest/userguide/snapshot-archive.html) in the *Amazon EBS User Guide*.
If you don't want to keep the AMI and its snapshots, you must deregister the AMI and
delete the snapshots. For more information, see [Deregister an AMI](./deregister-ami.html).

## Prerequisites

To disable or re-enable an AMI, you must be the owner of the AMI.

## Required IAM permissions

To disable and re-enable an AMI, you must have the following IAM permissions:

-
`ec2:DisableImage`

-
`ec2:EnableImage`


## Disable an AMI

You can disable an AMI by using the EC2 console or the AWS Command Line Interface (AWS CLI). You must be the AMI owner to perform this procedure.

## Describe disabled AMIs

You can view disabled AMIs in the EC2 console and by using the AWS CLI.

You must be the AMI owner to view disabled AMIs. Because disabled AMIs are made private, you can't view disabled AMIs if you're not the owner.

## Re-enable a disabled AMI

You can re-enable a disabled AMI. You must be the AMI owner to perform this procedure.