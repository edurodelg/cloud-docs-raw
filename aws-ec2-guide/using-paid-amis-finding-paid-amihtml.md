---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-paid-amis-finding-paid-ami.html
fetched_at: 2026-02-05T08:19:33.436905
---

# Find a paid AMI

A paid AMI is an Amazon Machine Image (AMI) that is available for purchase. A paid AMI also has a product code. You can find AMIs that are available for purchase in the AWS Marketplace.

- Console
-
###### To find a paid AMI

-
Open the Amazon EC2 console at

[https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/). -
In the navigation pane, choose

**AMIs**. -
Choose

**Public images**for the first filter. -
Do one of the following:

-
If you know the product code, choose

**Product code**, then**=**, and then enter the product code. -
If you do not know the product code, in the Search bar, specify the following filter:

**Owner alias=aws-marketplace**. Specify additional filters as needed.

-
-
Save the ID of the AMI.


-
- AWS CLI
-
###### To find a paid AMI

Use the following

[describe-images](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-images.html)command.`aws ec2 describe-images --owners aws-marketplace`

The output includes a large number of images. You can specify filters to help you determine which AMI you need. After you find an AMI, specify its ID in the following command to get its product code.

`aws ec2 describe-images \ --image-ids`

`ami-0abcdef1234567890`

\ --query Images[*].ProductCodes[].ProductCodeIdThe following is example output.

`[ "cdef1234abc567def8EXAMPLE" ]`

If you know the product code, you can filter the results by product code. This example returns the most recent AMI with the specified product code.

`aws ec2 describe-images \ --filters "Name=product-code,Values=`

`cdef1234abc567def8EXAMPLE`

" \ --query "sort_by(Images, &CreationDate)[-1].[ImageId]" - PowerShell
-
###### To find a paid AMI

Use the

[Get-EC2Image](https://docs.aws.amazon.com/powershell/latest/reference/items/Get-EC2Image.html)cmdlet.`Get-EC2Image -Owner aws-marketplace`

The output includes a large number of images. You can specify filters to help you determine which AMI you need. After you find an AMI, specify its ID in the following command to get its product code.

`(Get-EC2Image -ImageId`

`ami-0abcdef1234567890`

).ProductCodesThe following is example output.

`ProductCodeId ProductCodeType ------------- --------------- cdef1234abc567def8EXAMPLE marketplace`

If you know the product code, you can filter the results by product code. This example returns the most recent AMI with the specified product code.

`(Get-EC2Image -Owner aws-marketplace -Filter @{"Name"="product-code";"Value"="`

`cdef1234abc567def8EXAMPLE`

"} | sort CreationDate -Descending | Select-Object -First 1).ImageId