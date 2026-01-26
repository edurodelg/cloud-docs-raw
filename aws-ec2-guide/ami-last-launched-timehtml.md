---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ami-last-launched-time.html
fetched_at: 2026-01-26T22:58:45.734090
---

# Check when an Amazon EC2 AMI was last used

Amazon EC2 automatically tracks the date and time when an AMI was last used to launch an
instance. If you have an AMI that has not been used to launch an instance in a long
time, consider whether the AMI is a good candidate for [deregistration](./deregister-ami.html) or [deprecation](./ami-deprecate.html).

###### Considerations

-
When an AMI is used to launch an instance, there is a 24-hour delay before that usage is reported.

-
You must be the owner of the AMI to get the last launched time.

-
AMI usage data is available starting April 2017.