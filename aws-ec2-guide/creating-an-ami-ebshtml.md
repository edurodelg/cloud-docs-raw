---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-an-ami-ebs.html
fetched_at: 2026-02-05T08:20:03.714476
---

# Create an Amazon EBS-backed AMI

You can create your own Amazon EBS-backed AMI from an Amazon EC2 instance or from a snapshot of the
root volume of an Amazon EC2 instance.

To create an Amazon EBS-backed AMI from an instance, start by launching an instance using an
existing Amazon EBS-backed AMI. This AMI can be one you obtained from the AWS Marketplace, created using
[VM Import/Export](https://docs.aws.amazon.com/vm-import/latest/userguide/what-is-vmimport.html), or any other AMI
that you can access. After customizing the instance to meet your specific requirements,
create and register a new AMI. You can then use the new AMI to launch new instances with
your customizations.

To create an AMI that supports EC2 instance attestation, see [Attestable AMIs](./attestable-ami.html).

The procedures described below work for Amazon EC2 instances backed by encrypted Amazon Elastic Block Store
(Amazon EBS) volumes (including the root volume) as well as for unencrypted volumes.

The AMI creation process is different for Amazon S3-backed AMIs. For more information, see
[Create an Amazon S3-backed AMI](./creating-an-ami-instance-store.html).

## Overview of AMI creation from an instance

The following diagram summarizes the process for creating an Amazon EBS-backed AMI from a
running EC2 instance: Start with an existing AMI, launch an instance, customize it,
create a new AMI from it, and finally launch an instance of your new AMI. The
numbers in the diagram match the numbers in the description that follows.

**1 – AMI #1: Start with an existing
AMI**
-
Find an existing AMI that is similar to the AMI that you'd like to create.
This can be an AMI you have obtained from the AWS Marketplace, an AMI that you have created
using [VM Import/Export](https://docs.aws.amazon.com/vm-import/latest/userguide/what-is-vmimport.html), or any
other AMI that you can access. You'll customize this AMI for your needs.

In the diagram, **EBS root volume snapshot #1** indicates
that the AMI is an Amazon EBS-backed AMI and that information about the root
volume is stored in this snapshot.

**2 – Launch instance from existing
AMI**
-
The way to configure an AMI is to launch an instance from the AMI on
which you'd like to base your new AMI, and then customize the instance
(indicated at **3** in the diagram). Then, you'll create a
new AMI that includes the customizations (indicated at
**4** in the diagram).

**3 – EC2 instance #1: Customize the
instance**
-
Connect to your instance and customize it for your needs. Your new AMI
will include these customizations.

You can perform any of the following actions on your instance to customize
it:

-
Install software and applications

-
Copy data

-
Reduce start time by deleting temporary files and defragmenting
your hard drive

-
Attach additional EBS volumes


**4 – Create image**
-
When you create an AMI from an instance, Amazon EC2 powers down the instance
before creating the AMI to ensure that everything on the instance is
stopped and in a consistent state during the creation process. If you're
confident that your instance is in a consistent state appropriate for AMI
creation, you can tell Amazon EC2 not to power down and reboot the instance. Some
file systems, such as XFS, can freeze and unfreeze activity, making it safe
to create the image without rebooting the instance.

During the AMI-creation process, Amazon EC2 creates snapshots of your
instance's root volume and any other EBS volumes attached to your instance.
You're charged for the snapshots until you [deregister the AMI](./deregister-ami.html)
and delete the snapshots. If any volumes attached to the
instance are encrypted, the new AMI only launches successfully on
instances that support Amazon EBS encryption.

Depending on the size of the volumes, it can take several minutes for the AMI-creation
process to complete (sometimes up to 24 hours). You might find it more
efficient to create snapshots of your volumes before creating your AMI.
This way, only small, incremental snapshots need to be created when the
AMI is created, and the process completes more quickly (the total time for
snapshot creation remains the same).

**5 – AMI #2: New AMI**
-
After the process completes, you have a new AMI and snapshot (**snapshot
#2**) created from the root volume of the instance. If you
added instance store volumes or EBS volumes to the instance, in addition to
the root volume, the block device mapping for the new AMI contains
information for these volumes.

Amazon EC2 automatically registers the AMI for you.

**6 – Launch instance from new
AMI**
-
You can use the new AMI to launch an instance.

**7 – EC2 instance #2: New
instance**
-
When you launch an instance using the new AMI, Amazon EC2 creates a new EBS volume for the
instance's root volume using the snapshot. If you added instance store
volumes or EBS volumes when you customized the instance, the block device
mapping for the new AMI contains information for these volumes, and the
block device mappings for instances that you launch from the new AMI
automatically contain information for these volumes. The instance store
volumes specified in the block device mapping for the new instance are new
and don't contain any data from the instance store volumes of the instance
you used to create the AMI. The data on EBS volumes persists. For more
information, see [Block device mappings for volumes on Amazon EC2 instances](./block-device-mapping-concepts.html).

When you create a new instance from an EBS-backed AMI, you should
initialize both its root volume and any additional EBS storage before
putting it into production. For more information, see [Initialize Amazon EBS volumes](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-initialize.html)
in the *Amazon EBS User Guide*.


## Create an AMI from an instance

If you have an existing instance, you can create an AMI from this instance.

- Console
-
###### To create an AMI

-
Open the Amazon EC2 console at
[https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).

-
In the navigation pane, choose
**Instances**.

-
Select the instance from which to create the AMI, and then choose
**Actions**, **Image and
templates**, **Create image**.

If this option is disabled, your instance isn't an
Amazon EBS-backed instance.

-
On the **Create image** page, specify the
following information:

-
For **Image name**, enter a unique name
for the image, up to 127 characters.

-
For **Image description**, enter an
optional description of the image, up to 255
characters.

-
For **Reboot instance**, either keep the checkbox selected (the
default), or clear it.

-
If **Reboot instance** is selected, when Amazon EC2 creates the new
AMI, it reboots the instance so that it can take
snapshots of the attached volumes while data is at
rest, in order to ensure a consistent state.

-
If **Reboot instance** is cleared, when Amazon EC2 creates the new AMI,
it does not shut down and reboot the
instance.


If you clear **Reboot instance**, we can't guarantee the file system
integrity of the created image.

-
**Instance volumes** – You can
modify the root volume, and add additional Amazon EBS and
instance store volumes, as follows:

-
The root volume is defined in the first
row.

-
To change the size of the root volume, for
**Size**, enter the required
value.

-
If you select **Delete on
termination**, when you terminate the
instance created from this AMI, the EBS volume is
deleted. If you clear **Delete on
termination**, when you terminate the
instance, the EBS volume is not deleted. For more
information, see [Preserve data when an instance is
terminated](./preserving-volumes-on-termination.html).


-
To add an EBS volume, choose **Add
volume** (which adds a new row). For
**Storage type**, choose
**EBS**, and fill in the fields
in the row. When you launch an instance from your
new AMI, additional volumes are automatically
attached to the instance. Empty volumes must be
formatted and mounted. Volumes based on a snapshot
must be mounted.

-
To add an instance store volume, see [Add instance store volumes to an Amazon EC2 AMI](./adding-instance-storage-ami.html).
When you launch an instance from your new AMI,
additional volumes are automatically initialized and
mounted. These volumes do not contain data from the
instance store volumes of the running instance on
which you based your AMI.


-
**Snapshot destination** – If your instance volumes are in a
Local Zone that supports EBS local snapshots, choose where
to create the AMI’s snapshots:

This option appears only in Local Zones that support EBS local snapshots, and only
if your instance was created in a Local Zone. If the
volume is in a Region, this option does not appear, and
the snapshot is automatically created in the same Region
as the volume. For more information, see [Local snapshots in Local Zones](https://docs.aws.amazon.com/ebs/latest/userguide/snapshots-localzones.html) in the
*Amazon EBS User Guide*.

All snapshots of the instance’s volumes must be in the same location. Verify the
location of existing snapshots. If any existing
snapshots are in a different location than your selected
destination, the AMI creation will fail.

-
**Tags** – You can tag the AMI and
the snapshots with the same tags, or you can tag them with
different tags.

-
To tag the AMI and the snapshots with the
*same* tags,
choose **Tag image and snapshots
together**. The same tags are applied to
the AMI and every snapshot that is created.

-
To tag the AMI and the snapshots with *different* tags, choose
**Tag image and snapshots
separately**. Different tags are applied
to the AMI and the snapshots that are created.
However, all the snapshots get the same tags; you
can't tag each snapshot with a different tag.


To add a tag, choose **Add tag**, and
enter the key and value for the tag. Repeat for each
tag.

-
When you're ready to create your AMI, choose
**Create image**.


-
To view the status of your AMI while it is being created:

-
In the navigation pane, choose
**AMIs**.

-
Set the filter to **Owned by me**, and
find your AMI in the list.

Initially, the status is `pending`

but should
change to `available`

after a few minutes.


-
(Optional) To view the snapshot that was created for the new
AMI:

-
Note the ID of your AMI that you located in the previous
step.

-
In the navigation pane, choose
**Snapshots**.

-
Set the filter to **Owned by me**, and
then find the snapshot with the new AMI ID in the
**Description** column.

When you launch an instance from this AMI, Amazon EC2 uses this snapshot to create the
instance's root volume.


- AWS CLI
-
###### To create an AMI

Use the [create-image](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-image.html) command.

```
aws ec2 create-image \
--instance-id
````i-1234567890abcdef0`

\
--name "`my-web-server`

" \
--description "`My web server image`

" \
--no-reboot


- PowerShell
-
###### To create an AMI

Use the [New-EC2Image](https://docs.aws.amazon.com/powershell/latest/reference/items/New-EC2Image.html) cmdlet.

```
New-EC2Image `
-InstanceId
````i-1234567890abcdef0`

`
-Name `"my-web-server"`

`
-Description "`My web server image`

" `
-NoReboot $true


## Create an AMI from a snapshot

If you have a snapshot of the root volume of an instance, you can create an AMI from this
snapshot.

In most cases, AMIs for Windows, Red Hat, SUSE, and SQL Server require correct
licensing information to be present on the AMI. For more information, see [Understand AMI billing information](./ami-billing-info.html). When creating an
AMI from a snapshot, the `RegisterImage`

operation derives the correct
billing information from the snapshot's metadata, but this requires the appropriate
metadata to be present. To verify if the correct billing information was applied,
check the **Platform details** field on the new AMI. If the field
is empty or doesn't match the expected operating system code (for example, Windows,
Red Hat, SUSE, or SQL), the AMI creation was unsuccessful, and you should discard
the AMI and follow the instructions in [Create an AMI from an instance](#how-to-create-ebs-ami).

- Console
-
###### To create an AMI from a snapshot

Open the Amazon EC2 console at
[https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).

-
In the navigation pane, choose
**Snapshots**.

-
Select the snapshot from which to create the AMI, and then
choose **Actions**, **Create image from
snapshot**.

-
On the **Create image from snapshot** page,
specify the following information:

-
For **Image name**, enter a descriptive
name for the image.

-
For **Description**, enter a brief
description for the image.

-
For **Architecture**, choose the image
architecture. Choose **i386** for 32-bit,
**x86_64** for 64-bit,
**arm64** for 64-bit ARM, or
**x86_64** for 64-bit macOS.

-
For **Root device name**, enter the device name to use for the root
volume. For more information, see [Device names for volumes on Amazon EC2 instances](./device_naming.html).

-
For **Virtualization type**, choose the
virtualization type to be used by instances launched from
this AMI. For more information, see [Virtualization types](./ComponentsAMIs.html#virtualization_types).

-
(For paravirtual virtualization only) For **Kernel ID**, select the
operating system kernel for the image. If you're using a
snapshot of the root volume of an instance, select the same
kernel ID as the original instance. If you're unsure, use
the default kernel.

-
(For paravirtual virtualization only) For **RAM
disk ID**, select the RAM disk for the image.
If you select a specific kernel, you may need to select a
specific RAM disk with the drivers to support it.

-
For **Boot mode**, choose the boot mode
for the image, or choose **Use default** so
that when an instance is launched with this AMI, it boots
with the boot mode supported by the instance type. For more
information, see [Set the boot mode of an Amazon EC2 AMI](./set-ami-boot-mode.html).

-
(Optional) Under **Block device mappings**,
customize the root volume and add additional data volumes.

For each volume, you can specify the size, type, performance
characteristics, the behavior of delete on termination, and
encryption status. For the root volume, the size can't be
smaller than the size of the snapshot. For volume type, General Purpose SSD
`gp3`

is the default selection.

-
(Optional) Under **Tags**, you can add one or more tags
to the new AMI. To add a tag, choose **Add
tag**, and enter the key and value for the tag.
Repeat for each tag.

-
When you're ready to create your AMI, choose
**Create image**.


-
(Windows, Red Hat, SUSE, and SQL Server only) To verify if the correct billing
information was applied, check the **Platform
details** field on the new AMI. If the field is empty
or doesn't match the expected operating system code (for example,
**Windows** or **Red Hat**),
the AMI creation was unsuccessful, and you should discard the AMI
and follow the instructions in [Create an AMI from an instance](#how-to-create-ebs-ami).


- AWS CLI
-
###### To create an AMI from a snapshot using the AWS CLI

Use the [register-image](https://docs.aws.amazon.com/cli/latest/reference/ec2/register-image.html) command.

```
aws ec2 register-image \
--name
````my-image`

\
--root-device-name `/dev/xvda`

\
--block-device-mappings DeviceName=`/dev/xvda`

,Ebs={SnapshotId=`snap-0db2cf683925d191f`

}


- PowerShell
-
###### To create an AMI from a snapshot using PowerShell

Use the [Register-EC2Image](https://docs.aws.amazon.com/powershell/latest/reference/items/Register-EC2Image.html) cmdlet.

`$block = @{SnapshotId=``snap-0db2cf683925d191f`

}
Register-EC2Image `
-Name `my-image`

`
-RootDeviceName `/dev/xvda`

`
-BlockDeviceMapping @{DeviceName="/dev/xvda";Ebs=$block}