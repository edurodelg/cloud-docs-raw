---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/your-ec2-ami-usage.html
fetched_at: 2026-02-06T16:40:18.141798
---

# View your AMI usage

###### To list all the AMI usage reports for the specified AMI

Use the [describe-image-usage-reports](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-image-usage-reports.html) command and specify the ID of
the AMI to get a list of its reports.

`aws ec2 describe-image-usage-reports --image-ids ``ami-0abcdef1234567890`


The following is example output. Each report ID is listed along with the resource types
that were scanned and the report creation and expiration dates. You can use
this information to identify the reports whose entries you want to
view.

```
{
"ImageUsageReports": [
{
"ImageId": "ami-0abcdef1234567890",
"ReportId": "amiur-1111111111111111",
"ResourceTypes": [
{
"ResourceType": "ec2:Instance"
}
],
"State": "available",
"CreationTime": "2025-09-29T13:27:12.322000+00:00",
"ExpirationTime": "2025-10-28T13:27:12.322000+00:00",
"Tags": []
},
{
"ImageId": "ami-0abcdef1234567890",
"ReportId": "amiur-22222222222222222",
"ResourceTypes": [
{
"ResourceType": "ec2:Instance"
},
{
"ResourceType": "ec2:LaunchTemplate"
}
],
"State": "available",
"CreationTime": "2025-10-01T13:27:12.322000+00:00",
"ExpirationTime": "2025-10-30T13:27:12.322000+00:00",
"Tags": []
}
],
"NextToken": "opaque"
}
```


###### To view the contents of an AMI usage report for the specified AMI

Use the [describe-image-usage-report-entries](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-image-usage-report-entries.html) command and specify the
ID of the AMI. The response returns all the reports for the specified
AMI, showing the accounts that have used the AMI and their resource
counts.

`aws ec2 describe-image-usage-report-entries --image-ids ``ami-0abcdef1234567890`


The following is example output.

```
{
"ImageUsageReportEntries": [
{
"ImageId": "ami-0abcdef1234567890",
"ResourceType": "ec2:Instance",
"AccountId": "123412341234",
"UsageCount": 15,
"ReportCreationTime": "2025-09-29T13:27:12.322000+00:00",
"ReportId": "amiur-1111111111111111"
},
{
"ImageId": "ami-0abcdef1234567890",
"ResourceType": "ec2:Instance",
"AccountId": "123412341234",
"UsageCount": 2,
"ReportCreationTime": "2025-10-01T13:27:12.322000+00:00",
"ReportId": "amiur-22222222222222222"
},
{
"ImageId": "ami-0abcdef1234567890",
"ResourceType": "ec2:Instance",
"AccountId": "001100110011",
"UsageCount": 39,
"ReportCreationTime": "2025-10-01T13:27:12.322000+00:00",
"ReportId": "amiur-22222222222222222"
}
],
"NextToken": "opaque"
}
```


###### To view the contents of an AMI usage report for the specified report

Use the [describe-image-usage-report-entries](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-image-usage-report-entries.html) command and specify the
ID of the report. The response returns all the entries for the specified
report, showing the accounts that have used the AMI and their resource
counts.

`aws ec2 describe-image-usage-report-entries --report-ids ``amiur-11111111111111111`


The following is example output.

```
{
"ImageUsageReportEntries": [
{
"ImageId": "ami-0abcdef1234567890",
"ResourceType": "ec2:Instance",
"AccountId": "123412341234",
"UsageCount": 15,
"ReportCreationTime": "2025-09-29T13:27:12.322000+00:00",
"ReportId": "amiur-11111111111111111"
},
{
"ImageId": "ami-0abcdef1234567890",
"ResourceType": "ec2:LaunchTemplate",
"AccountId": "123412341234",
"UsageCount": 4,
"ReportCreationTime": "2025-09-29T13:27:12.322000+00:00",
"ReportId": "amiur-11111111111111111"
},
{
"ImageId": "ami-0abcdef1234567890",
"ResourceType": "ec2:LaunchTemplate",
"AccountId": "001100110011",
"UsageCount": 2,
"ReportCreationTime": "2025-09-29T13:27:12.322000+00:00",
"ReportId": "amiur-11111111111111111"
}
],
"NextToken": "opaque"
}
```


###### To list all the AMI usage reports for the specified AMI

Use the [Get-EC2ImageUsageReport](https://docs.aws.amazon.com/powershell/latest/reference/items/Get-EC2ImageUsageReport.html) cmdlet and specify the ID of the
AMI to get a list of its reports.

`Get-EC2ImageUsageReport -ImageId ``ami-0abcdef1234567890`


The following is example output. Each report ID is listed along with the resource types
that were scanned and the report creation and expiration dates. You can use
this information to identify the reports whose entries you want to
view.

```
@{
ImageUsageReports = @(
@{
ImageId = "ami-0abcdef1234567890"
ReportId = "amiur-1111111111111111"
ResourceTypes = @(
@{
ResourceType = "ec2:Instance"
}
)
State = "available"
CreationTime = "2025-09-29T13:27:12.322000+00:00"
ExpirationTime = "2025-10-28T13:27:12.322000+00:00"
},
@{
ImageId = "ami-0abcdef1234567890"
ReportId = "amiur-22222222222222222"
ResourceTypes = @(
@{
ResourceType = "ec2:Instance"
}
)
State = "available"
CreationTime = "2025-09-30T13:27:12.322000+00:00"
ExpirationTime = "2025-10-29T13:27:12.322000+00:00"
},
@{
ImageId = "ami-0abcdef1234567890"
ReportId = "amiur-33333333333333333"
ResourceTypes = @(
@{
ResourceType = "ec2:Instance"
}
)
State = "available"
CreationTime = "2025-10-01T13:27:12.322000+00:00"
ExpirationTime = "2025-10-30T13:27:12.322000+00:00"
}
)
NextToken = "opaque"
}
```


###### To view the contents of an AMI usage report for the specified AMI

Use the [Get-EC2ImageUsageReportEntry](https://docs.aws.amazon.com/powershell/latest/reference/items/Get-EC2ImageUsageReportEntry.html) cmdlet and specify the ID of
the AMI. The response returns all the reports for the specified AMI,
showing the accounts that have used the AMI and their resource
counts.

`Get-EC2ImageUsageReportEntry -ImageId ``ami-0abcdef1234567890`


The following is example output.

```
ImageUsageReportEntries : {@{
ImageId = "ami-0abcdef1234567890"
ResourceType = "ec2:Instance"
AccountId = "123412341234"
UsageCount = 15
ReportCreationTime = "2025-09-29T13:27:12.322000+00:00"
ReportId = "amiur-1111111111111111"
}, @{
ImageId = "ami-0abcdef1234567890"
ResourceType = "ec2:Instance"
AccountId = "123412341234"
UsageCount = 7
ReportCreationTime = "2025-09-30T13:27:12.322000+00:00"
ReportId = "amiur-22222222222222222"
}...}
NextToken : opaque
```


###### To view the contents of an AMI usage report for the specified report

Use the [Get-EC2ImageUsageReportEntry](https://docs.aws.amazon.com/powershell/latest/reference/items/Get-EC2ImageUsageReportEntry.html) cmdlet and specify the ID of
the report. The response returns all the entries for the specified
report, showing the accounts that have used the AMI and their resource
counts.

`Get-EC2ImageUsageReportEntry -ReportId ``amiur-11111111111111111`


The following is example output.

```
ImageUsageReportEntries : {@{
ImageId = "ami-0abcdef1234567890"
ResourceType = "ec2:Instance"
AccountId = "123412341234"
UsageCount = 15
ReportCreationTime = "2025-09-29T13:27:12.322000+00:00"
ReportId = "amiur-11111111111111111"
}, @{
ImageId = "ami-0abcdef1234567890"
ResourceType = "ec2:LaunchTemplate"
AccountId = "123412341234"
UsageCount = 4
ReportCreationTime = "2025-09-29T13:27:12.322000+00:00"
ReportId = "amiur-11111111111111111"
}, @{
ImageId = "ami-0abcdef1234567890"
ResourceType = "ec2:LaunchTemplate"
AccountId = "************"
UsageCount = 2
ReportCreationTime = "2025-09-29T13:27:12.322000+00:00"
ReportId = "amiur-11111111111111111"
}}
NextToken : opaque
```