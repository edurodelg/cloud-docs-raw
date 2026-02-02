---
source_url: https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-object-metadata.html
fetched_at: 2026-02-02T15:54:07.088238
---

# Editing object metadata in the Amazon S3 console

You can use the Amazon S3 console to edit metadata for existing S3 objects by using the **Copy** action. To edit metadata, you copy objects to the same destination and specify the new metadata you want to apply, which replaces the old metadata for the object. Some metadata is set
by Amazon S3 when you upload the object. For example, `Content-Length`

and
`Last-Modified`

are system-defined object metadata fields that can't be modified by
a user.

You can also set user-defined metadata when you upload the object and replace it as your needs
change. For example, you might have a set of objects that you initially store in the
`STANDARD`

storage class. Over time, you may no longer need this data to be
highly available. So, you can change the storage class to `GLACIER`

by replacing the value
of the `x-amz-storage-class`

key from `STANDARD`

to
`GLACIER`

.

###### Note

Consider the following when you are replacing object metadata in Amazon S3:

-
You must specify existing metadata you want to retain, metadata you want to add, and metadata you want to edit.

-
If your object is less than 5 GB, you can use the

**Copy**action in the S3 console to replace object metadata. If your object is greater than 5 GB, you can replace the object metadata when you copy an object with multipart upload by using the[AWS CLI](./mpu-upload-object.html#UsingCLImpUpload)or[AWS SDKs](./CopyingObjectsMPUapi.html). For more information, see[Copying an object using multipart upload](./CopyingObjectsMPUapi.html). -
For a list of additional permissions required to replace metadata, see

[Required permissions for Amazon S3 API operations](./using-with-s3-policy-actions.html). For example policies that grant this permission, see[Identity-based policy examples for Amazon S3](./example-policies-s3.html). -
This action creates a

*copy*of the object with updated settings and the last-modified date. If S3 Versioning is enabled, a new version of the object is created, and the existing object becomes an older version. If S3 Versioning isn't enabled, a new copy of the object replaces the original object. The AWS account associated with the IAM role that changes the property also becomes the owner of the new object or (object version). -
Editing metadata replaces values for existing key names.

-
Objects that are encrypted with customer-provided encryption keys (SSE-C) can't be copied by using the console. You must use the AWS CLI, AWS SDK, or the Amazon S3 REST API.

-
When copying an object by using the Amazon S3 console, you might receive the error message

The console uses headers to retrieve and set metadata for your object. If your network or browser configuration modifies your network requests, this behavior might cause unintended metadata (such as modified`"Copied metadata can't be verified."`

`Cache-Control`

headers) to be written to your copied object. Amazon S3 can't verify this unintended metadata.To address this issue, check your network and browser configuration to make sure it doesn't modify headers, such as

`Cache-Control`

. For more information, see[The Shared Responsibility Model](https://docs.aws.amazon.com/whitepapers/latest/applying-security-practices-to-network-workload-for-csps/the-shared-responsibility-model.html).

###### Warning

When replacing metadata for folders, wait for the **Copy** action to
finish before adding new objects to the folder. Otherwise, new objects might also be
edited.

The following topics describe how to replace metadata for an object by using the **Copy** action in the Amazon S3
console.

You can replace some system-defined metadata for an S3 object. For a list of
system-defined metadata and values that you can modify, see [System-defined object metadata](./UsingMetadata.html#SysMetadata).

###### To replace system-defined metadata of an object

Sign in to the AWS Management Console and open the Amazon S3 console at

[https://console.aws.amazon.com/s3/](https://console.aws.amazon.com/s3/).-
In the left navigation pane, choose

**General purpose buckets**or**Directory buckets**. -
In the list of buckets, choose the name of the bucket that contains the objects you want to change.

-
Select the check box for the objects you want to change.

-
On the

**Actions**menu, choose**Copy**from the list of options that appears. -
To specify the destination path, choose

**Browse S3**, navigate to the same destination as the source objects, and select the destination check box. Choose**Choose destination**in the lower-right corner.Alternatively, enter the destination path.

-
If you do

*not*have bucket versioning enabled, you will see a warning recommending you enable Bucket Versioning to help protect against unintentionally overwriting or deleting objects. If you want to keep all versions of objects in this bucket, select**Enable Bucket Versioning**. You can also view the default encryption and Object Lock properties in**Destination details**. -
Under

**Additional copy settings**, choose**Specify settings**to specify settings for**Metadata**. Scroll to the

**Metadata**section, and then choose**Replace all metadata**.-
Choose

**Add metadata**. -
For metadata

**Type**, select**System-defined**. -
Specify a unique

**Key**and the metadata**Value**. -
To edit additional metadata, choose

**Add metadata**. You can also choose**Remove**to remove a set of type-key-values. -
Choose

**Copy**. Amazon S3 saves your metadata changes.

You can replace user-defined metadata of an object by combining the metadata prefix,
`x-amz-meta-`

, and a name you choose to create a custom key. For example, if
you add the custom name `alt-name`

, the metadata key would be
`x-amz-meta-alt-name`

.

User-defined metadata can be as large as 2 KB total. To calculate the total size of
user-defined metadata, sum the number of bytes in the UTF-8 encoding for each key and value.
Both keys and their values must conform to US-ASCII standards. For more information, see
[User-defined object metadata](./UsingMetadata.html#UserMetadata).

###### To replace user-defined metadata of an object

Sign in to the AWS Management Console and open the Amazon S3 console at

[https://console.aws.amazon.com/s3/](https://console.aws.amazon.com/s3/).-
In the navigation pane, choose

**Buckets**, and then choose the**General purpose buckets**or**Directory buckets**tab. Navigate to the Amazon S3 bucket or folder that contains the objects you want to change. -
Select the check box for the objects you want to change.

-
On the

**Actions**menu, choose**Copy**from the list of options that appears. -
To specify the destination path, choose

**Browse S3**, navigate to the same destination as the source objects, and select the destination check box. Choose**Choose destination**.Alternatively, enter the destination path.

-
If you do

*not*have bucket versioning enabled, you will see a warning recommending you enable Bucket Versioning to help protect against unintentionally overwriting or deleting objects. If you want to keep all versions of objects in this bucket, select**Enable Bucket Versioning**. You can also view the default encryption and Object Lock properties in**Destination details**. -
Under

**Additional copy settings**, choose**Specify settings**to specify settings for**Metadata**. Scroll to the

**Metadata**section, and then choose**Replace all metadata**.-
Choose

**Add metadata**. -
For metadata

**Type**, choose**User-defined**. -
Enter a unique custom

**Key**following`x-amz-meta-`

. Also enter a metadata**Value**. -
To add additional metadata, choose

**Add metadata**. You can also choose**Remove**to remove a set of type-key-values. -
Choose

**Copy**. Amazon S3 saves your metadata changes.