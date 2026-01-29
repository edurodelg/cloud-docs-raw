---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/display-ami-root-device-type.html
fetched_at: 2026-01-29T15:15:31.722334
---

# Identify the root volume type determined by your
					AMI

# Identify the root volume type determined by your
AMI

The AMI that you use to launch an EC2 instance determines the type of the root volume.
The root volume of an EC2 instance is either an EBS volume or an instance store volume.

[Nitro-based instances](./instance-types.html#instance-hypervisor-type) support only EBS root volumes. The following previous generation
instance types are the only instance types that support instance store root volumes:
C1, C3, D2, I2, M1, M2, M3, R3, and X1.

- Console
-
###### To identify the root volume type determined by an AMI

-
Open the Amazon EC2 console at
[https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).

-
In the navigation pane, choose **AMIs**, and select the AMI.

-
On the **Details** tab, check the value of **Root device
type** as follows:


- AWS CLI
-
###### To identify the root volume type determined by an AMI

Use the [describe-images](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-images.html)
command.

```
aws ec2 describe-images \
--image-ids
````ami-0abcdef1234567890`

\
--query Images[].RootDeviceType


The following is example output.

`ebs`


- PowerShell
-
###### To identify the root volume type determined by an AMI

Use the [Get-EC2Image](https://docs.aws.amazon.com/powershell/latest/reference/items/Get-EC2Image.html)
cmdlet.

```
(Get-EC2Image `
-ImageId
````ami-0abcdef1234567890`

).RootDeviceType.Value


The following is example output.

`ebs`