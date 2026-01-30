---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/marketplace-manage-subscriptions.html
fetched_at: 2026-01-30T23:35:15.188461
---

# Manage your AWS Marketplace
				subscriptions

# Manage your AWS Marketplace subscriptions

On the AWS Marketplace website, you can check your subscription details, view the vendor's usage instructions, manage your subscriptions, and more.

## Check subscription details

###### To check your subscription details

Log in to the

[AWS Marketplace](https://aws.amazon.com/marketplace).-
Choose

**Your Marketplace Account**. -
Choose

**Manage your software subscriptions**. -
All your current subscriptions are listed. Choose

**Usage Instructions**to view specific instructions for using the product, for example, a username for connecting to your running instance.

## Cancel subscription

###### Note

-
Canceling a subscription does not terminate the instances launched with that AMI. We'll continue to bill you for your running instances until they're terminated. You must terminate all instances launched with the AMI in order to stop billing for the subscription.

-
After you've canceled your subscription, you are no longer able to launch any instances from that AMI. To use that AMI again, you need to resubscribe to it, either on the AWS Marketplace website, or through the launch wizard in the Amazon EC2 console.


###### To cancel an AWS Marketplace subscription

-
To stop billing for the subscription, ensure that you have terminated any instances running from the subscription.

###### Warning

**Terminating an instance is permanent and irreversible.**After you terminate an instance, you can no longer connect to it, and it can't be recovered. All attached Amazon EBS volumes that are configured to be deleted on termination are also permanently deleted and can't be recovered. All data stored on instance store volumes is permanently lost. For more information, see

[How instance termination works](./how-ec2-instance-termination-works.html).Before you terminate an instance, ensure that you have backed up all data that you need to retain after the termination to persistent storage.

Open the Amazon EC2 console at

[https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/).-
In the navigation pane, choose

**Instances**. -
Select the instance, and then choose

**Instance state**,**Terminate (delete) instance**. -
Choose

**Terminate (delete)**when prompted for confirmation.

Log in to the

[AWS Marketplace](https://aws.amazon.com/marketplace), and choose**Your Marketplace Account**, then**Manage your software subscriptions**.-
Choose

**Cancel subscription**. You are prompted to confirm your cancellation.