---
source_url: https://docs.aws.amazon.com/AmazonS3/latest/userguide/transfer-acceleration-examples.html
fetched_at: 2026-01-29T15:20:40.081674
---

# Enabling and using S3 Transfer Acceleration

You can use Amazon S3 Transfer Acceleration to transfer files quickly and securely over long distances between your client and an S3 general purpose bucket. You can enable Transfer Acceleration using the S3 console, the AWS Command Line Interface (AWS CLI), API, or the AWS SDKs.

This section provides examples of how to enable Amazon S3 Transfer Acceleration on a bucket and use the acceleration endpoint for the enabled bucket.

For more information about Transfer Acceleration requirements, see [Configuring fast, secure file transfers using
Amazon S3 Transfer Acceleration](./transfer-acceleration.html).

###### Note

If you want to compare accelerated and non-accelerated upload speeds, open the [ Amazon S3 Transfer Acceleration Speed Comparison tool](https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html).

The Speed Comparison tool uses multipart upload to transfer a file from your browser to various AWS Regions with and without Amazon S3 transfer acceleration. You can compare the upload speed for direct uploads and transfer accelerated uploads by Region.

###### To enable transfer acceleration for an S3 general purpose bucket

Sign in to the AWS Management Console and open the Amazon S3 console at

[https://console.aws.amazon.com/s3/](https://console.aws.amazon.com/s3/).-
In the left navigation pane, choose

**General purpose buckets**. -
In the

**General purpose buckets**list, choose the name of the bucket that you want to enable transfer acceleration for. -
Choose

**Properties**. -
Under

**Transfer acceleration**, choose**Edit**. -
Choose

**Enable**, and choose**Save changes**.

###### To access accelerated data transfers

-
After Amazon S3 enables transfer acceleration for your bucket, view the

**Properties**tab for the bucket. -
Under

**Transfer acceleration**,**Accelerated endpoint**displays the transfer acceleration endpoint for your bucket. Use this endpoint to access accelerated data transfers to and from your bucket.If you suspend transfer acceleration, the accelerate endpoint no longer works.


The following are examples of AWS CLI commands used for Transfer Acceleration. For
instructions on setting up the AWS CLI, see [Developing with Amazon S3 using the
AWS CLI](https://docs.aws.amazon.com/AmazonS3/latest/API/setup-aws-cli.html) in the *Amazon S3 API Reference*.

### Enabling Transfer Acceleration on a bucket

Use the AWS CLI [put-bucket-accelerate-configuration](https://docs.aws.amazon.com/cli/latest/reference/s3api/put-bucket-accelerate-configuration.html) command to enable or
suspend Transfer Acceleration on a bucket.

The following example sets `Status=Enabled`

to enable Transfer Acceleration on
a bucket named

. To suspend Transfer Acceleration, use
`amzn-s3-demo-bucket`

`Status=Suspended`

.


`$`

aws s3api put-bucket-accelerate-configuration --bucket`amzn-s3-demo-bucket`

--accelerate-configuration Status=Enabled

### Using Transfer Acceleration

You can direct all Amazon S3 requests made by `s3`

and `s3api`

AWS CLI commands to the accelerate endpoint: `s3-accelerate.amazonaws.com`

. To
do this, set the configuration value `use_accelerate_endpoint`

to
`true`

in a profile in your AWS Config file. Transfer Acceleration must be enabled
on your bucket to use the accelerate endpoint.

All requests are sent using the virtual style of bucket
addressing:

. Any
`amzn-s3-demo-bucket`

.s3-accelerate.amazonaws.com`ListBuckets`

, `CreateBucket`

, and `DeleteBucket`

requests are not sent to the accelerate endpoint because the endpoint doesn't support
those operations.

For more information about `use_accelerate_endpoint`

, see [AWS CLI S3 Configuration](https://docs.aws.amazon.com/cli/latest/topic/s3-config.html)
in the *AWS CLI Command Reference*.

The following example sets `use_accelerate_endpoint`

to `true`

in the default profile.


`$`

aws configure set default.s3.use_accelerate_endpoint true

If you want to use the accelerate endpoint for some AWS CLI commands but not others, you can use either one of the following two methods:

-
Use the accelerate endpoint for any

`s3`

or`s3api`

command by setting the`--endpoint-url`

parameter to`https://s3-accelerate.amazonaws.com`

. -
Set up separate profiles in your AWS Config file. For example, create one profile that sets

`use_accelerate_endpoint`

to`true`

and a profile that does not set`use_accelerate_endpoint`

. When you run a command, specify which profile you want to use, depending upon whether you want to use the accelerate endpoint.

### Uploading an object to a bucket enabled for Transfer Acceleration

The following example uploads a file to a bucket named

that's been enabled for Transfer Acceleration by using the
default profile that has been configured to use the accelerate endpoint.`amzn-s3-demo-bucket`


`$`

aws s3 cp`file.txt`

s3://`--region`

`amzn-s3-demo-bucket`

/key-name`region`


The following example uploads a file to a bucket enabled for Transfer Acceleration by
using the `--endpoint-url`

parameter to specify the accelerate
endpoint.


`$`

aws configure set s3.addressing_style virtual`$`

aws s3 cp`file.txt`

s3://`--region`

`amzn-s3-demo-bucket`

/key-name`region`

--endpoint-url https://s3-accelerate.amazonaws.com

The following are examples of using Transfer Acceleration to upload objects to Amazon S3 using
the AWS SDK. Some of the AWS SDK supported languages (for example, Java
and .NET) use an accelerate endpoint client configuration flag so you don't
need to explicitly set the endpoint for Transfer Acceleration to

.`bucket-name`

.s3-accelerate.amazonaws.com

Use the REST API `PutBucketAccelerateConfiguration`

operation to enable accelerate configuration on an existing bucket.

For more information, see [PutBucketAccelerateConfiguration](https://docs.aws.amazon.com/AmazonS3/latest/API/API_PutBucketAccelerateConfiguration.html) in the *Amazon Simple Storage Service API Reference*.