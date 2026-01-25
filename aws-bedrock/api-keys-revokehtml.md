---
source_url: https://docs.aws.amazon.com/bedrock/latest/userguide/api-keys-revoke.html
fetched_at: 2026-01-25T03:11:35.561530
---

# Handle compromised long-term and short-term Amazon Bedrock API keys

If your API key becomes compromised, you should revoke permissions to use it. There are various methods that you can use to revoke permissions for an Amazon Bedrock API key:

-
For long-term Amazon Bedrock API keys, you can use the [UpdateServiceSpecificCredential](https://docs.aws.amazon.com/IAM/latest/APIReference/API_UpdateServiceSpecificCredential.html.html), [ResetServiceSpecificCredential](https://docs.aws.amazon.com/IAM/latest/APIReference/API_ResetServiceSpecificCredential.html.html), or [DeleteServiceSpecificCredential](https://docs.aws.amazon.com/IAM/latest/APIReference/API_DeleteServiceSpecificCredential.html.html) to revoke permissions in the following ways:

-
Set the status of the key to inactive. You can reactivate the key later.

-
Reset the key. This action generates a new password for the key.

-
Delete the key permanently.


To carry out these actions through the API, you must authenticate with AWS credentials and not with an Amazon Bedrock API key.

-
For both long-term and short-term Amazon Bedrock API keys, you can attach IAM policies to revoke permissions.


## Change the status of a long-term Amazon Bedrock API key

If you need to prevent a key from being used temporarily, deactivate it. After you're ready for it to be used again, reactivate it.

Choose the tab for your preferred method, and then follow the steps:

- Console
-
###### To deactivate a key

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at
[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock).

-
In the left navigation pane, select **API keys**.

-
In the **Long-term API keys** section, choose a key whose **Status** is **Inactive**.

-
Choose **Actions**.

-
Select **Deactivate**.

-
To confirm, select **Deactivate API key**. The **Status** of the key becomes **Inactive**.


###### To reactivate a key

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at
[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock).

-
In the left navigation pane, select **API keys**.

-
In the **Long-term API keys** section, choose a key whose **Status** is **Inactive**.

-
Choose **Actions**.

-
Select **Activate**.

-
To confirm, select **Activate API key**. The **Status** of the key becomes **Active**.


- Python
-
To deactivate a key using the API, send an [UpdateServiceSpecificCredential](https://docs.aws.amazon.com/IAM/latest/APIReference/API_UpdateServiceSpecificCredential.html.html) request with an [IAM endpoint](https://docs.aws.amazon.com/general/latest/gr/iam-service.html) and specify the `Status`

as `Inactive`

. You can use the following code snippet to deactivate a key, replacing `${ServiceSpecificCredentialId}`

with the value returned when you created the key.

```
import boto3
iam_client = boto3.client("iam")
iam_client.update_service_specific_credential(
service_specific_credential_id=
````${ServiceSpecificCredentialId}`

,
status="Inactive"
)


To reactivate a key using the API, send an [UpdateServiceSpecificCredential](https://docs.aws.amazon.com/IAM/latest/APIReference/API_UpdateServiceSpecificCredential.html.html) request with an [IAM endpoint](https://docs.aws.amazon.com/general/latest/gr/iam-service.html) and specify the `Status`

as `Active`

. You can use the following code snippet to reactivate a key, replacing `${ServiceSpecificCredentialId}`

with the value returned when you created the key.

```
import boto3
iam_client = boto3.client("iam")
iam_client.update_service_specific_credential(
service_specific_credential_id=
````${ServiceSpecificCredentialId}`

,
status="Active"
)


## Reset a long-term Amazon Bedrock API key

If the value of your key has been compromised or you no longer have it, reset it. The key must not have expired yet. If it's already expired, delete the key and create a new one.

Choose the tab for your preferred method, and then follow the steps:

- Console
-
###### To reset a key

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at
[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock).

-
In the left navigation pane, select **API keys**.

-
In the **Long-term API keys** section, choose a key.

-
Choose **Actions**.

-
Select **Reset key**.

-
Select **Next**.


- Python
-
To reset a key using the API, send a [ResetServiceSpecificCredential](https://docs.aws.amazon.com/IAM/latest/APIReference/API_ResetServiceSpecificCredential.html.html) request with an [IAM endpoint](https://docs.aws.amazon.com/general/latest/gr/iam-service.html). You can use the following code snippet to reset a key, replacing `${ServiceSpecificCredentialId}`

with the value returned when you created the key.

```
import boto3
iam_client = boto3.client("iam")
iam_client.reset_service_specific_credential(
service_specific_credential_id=
````${ServiceSpecificCredentialId}`

)


## Delete a long-term Amazon Bedrock API key

If you no longer need a key or it has expired, delete it.

Choose the tab for your preferred method, and then follow the steps:

- Console
-
###### To delete a key

-
Sign in to the AWS Management Console with an IAM identity that has permissions to use the Amazon Bedrock console. Then, open the Amazon Bedrock console at
[https://console.aws.amazon.com/bedrock](https://console.aws.amazon.com/bedrock).

-
In the left navigation pane, select **API keys**.

-
In the **Long-term API keys** section, choose a key.

-
Choose **Actions**.

-
Select **Delete**.

-
Confirm the deletion.


- Python
-
To delete a key using the API, send a [DeleteServiceSpecificCredential](https://docs.aws.amazon.com/IAM/latest/APIReference/API_DeleteServiceSpecificCredential.html.html) request with an [IAM endpoint](https://docs.aws.amazon.com/general/latest/gr/iam-service.html). You can use the following code snippet to delete a key, replacing `${ServiceSpecificCredentialId}`

with the value returned when you created the key.

```
import boto3
iam_client = boto3.client("iam")
iam_client.delete_service_specific_credential(
service_specific_credential_id=
````${ServiceSpecificCredentialId}`

)


## Attach IAM policies to remove permissions for using an Amazon Bedrock API key

This section provides some IAM policies that you can use to restrict access to an Amazon Bedrock API key.

### Deny an identity the ability to make calls with an Amazon Bedrock API key

The action that allows an identity to make calls with an Amazon Bedrock API key is `bedrock:CallWithBearerToken`

. To prevent an identity from making calls with the Amazon Bedrock API key, you can attach an IAM policy on an identity depending the type of key:

The IAM policy that you can attach to the IAM identity is as follows:

- JSON
-
-
```
{
"Version":"2012-10-17",
"Statement": {
"Effect": "Deny",
"Action": "bedrock:CallWithBearerToken",
"Resource": "*"
}
}
```


### Invalidate an IAM role session

If a short-term key becomes compromised, you can prevent its usage by invalidating the role session that was used to generate the key. To invalidate the role session, attach the following policy to the IAM identity that generated the key. Replace `2014-05-07T23:47:00Z`

with the time after which you want the session to be invalidated.

- JSON
-
-
```
{
"Version":"2012-10-17",
"Statement": {
"Effect": "Deny",
"Action": "*",
"Resource": "*",
"Condition": {
"DateLessThan": {"aws:TokenIssueTime": "
````2014-05-07T23:47:00Z`

"}
}
}
}