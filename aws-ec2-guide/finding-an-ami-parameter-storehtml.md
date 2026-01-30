---
source_url: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami-parameter-store.html
fetched_at: 2026-01-30T23:34:45.567929
---

# Reference the latest AMIs using Systems Manager public parameters

AWS Systems Manager provides public parameters for public AMIs maintained by AWS. You can use the
public parameters when launching instances to ensure that you're using the latest AMIs.
For example, the public parameter
`/aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-arm64`

is available in all Regions and always points to the latest version of the
Amazon Linux 2023 AMI for arm64 architecture in a given Region.

The public parameters are available from the following paths:

For more information, see [Working with public parameters](https://docs.aws.amazon.com/systems-manager/latest/userguide/parameter-store-public-parameters.html) in the *AWS Systems Manager User Guide*.

## List the Amazon Linux AMIs

- AWS CLI
-
###### To list the Linux AMIs in the current AWS Region

Use the following [get-parameters-by-path](https://docs.aws.amazon.com/cli/latest/reference/ssm/get-parameters-by-path.html) command. The value for the `--path`

parameter is specific to Linux AMIs.

```
aws ssm get-parameters-by-path \
--path /aws/service/ami-amazon-linux-latest \
--query "Parameters[].Name"
```


- PowerShell
-
###### To list the Linux AMIs in the current AWS Region

Use the [Get-SSMParametersByPath](https://docs.aws.amazon.com/powershell/latest/reference/items/Get-SSMParametersByPath.html)
cmdlet.

```
Get-SSMParametersByPath `
-Path "/aws/service/ami-amazon-linux-latest" | `
Sort-Object Name | Format-Table Name
```


## List the Windows AMIs

- AWS CLI
-
###### To list the Windows AMIs in the current AWS Region

Use the following [get-parameters-by-path](https://docs.aws.amazon.com/cli/latest/reference/ssm/get-parameters-by-path.html) command. The value for the `--path`

parameter is specific to Windows AMIs.

```
aws ssm get-parameters-by-path \
--path /aws/service/ami-windows-latest \
--query "Parameters[].Name"
```


- PowerShell
-
###### To list the Windows AMIs in the current AWS Region

Use the [Get-SSMParametersByPath](https://docs.aws.amazon.com/powershell/latest/reference/items/Get-SSMParametersByPath.html)
cmdlet.

```
Get-SSMParametersByPath `
-Path "/aws/service/ami-windows-latest" | `
Sort-Object Name | Format-Table Name
```


## Launch an instance using a public parameter

To specify the public parameter when launching an instance, use the following syntax:
`resolve:ssm:``public-parameter`


, where
`resolve:ssm`

is the standard prefix and
`public-parameter`


is the path and name of
the public parameter.

- AWS CLI
-
###### To launch an instance using a public parameter

Use the [run-instances](https://docs.aws.amazon.com/cli/latest/reference/ec2/run-instances.html)
command with the `--image-id`

option. This example
specifies a Systems Manager public parameter for the image ID to launch an
instance using the latest Amazon Linux 2023 AMI

`--image-id resolve:ssm:``/aws/service/ami-amazon-linux-latest/al2023-ami-kernel-default-x86_64`


- PowerShell
-
###### To launch an instance using a public parameter

Use the [New-EC2Instance](https://docs.aws.amazon.com/powershell/latest/reference/items/New-EC2Instance.html)
cmdlet with the `-ImageId`

parameter. This example
specifies a Systems Manager public parameter for the image ID to launch an
instance using the latest AMI for Windows Server 2022.

`-ImageId "resolve:ssm:``/aws/service/ami-windows-latest/Windows_Server-2022-English-Full-Base`

"


For more examples that use Systems Manager parameters, see [Query for the latest Amazon Linux AMI IDs Using AWS Systems Manager Parameter Store](https://aws.amazon.com/blogs/compute/query-for-the-latest-amazon-linux-ami-ids-using-aws-systems-manager-parameter-store/)
and [Query for the Latest Windows AMI Using AWS Systems Manager Parameter Store](https://aws.amazon.com/blogs/mt/query-for-the-latest-windows-ami-using-systems-manager-parameter-store/).