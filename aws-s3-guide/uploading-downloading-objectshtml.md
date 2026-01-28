---
source_url: https://docs.aws.amazon.com/AmazonS3/latest/userguide/uploading-downloading-objects.html
fetched_at: 2026-01-28T07:13:08.063177
---

# Working with objects in
            Amazon S3

# Working with objects in Amazon S3

To store your data in Amazon S3, you work with resources known as buckets and objects. A
*bucket* is a container for objects. An *object* is a file and any metadata that describes that
file.

To store an object in Amazon S3, you create a bucket and then upload the object to a bucket. When the object is in the bucket, you can open it, download it, and copy it. When you no longer need an object or a bucket, you can clean up these resources.

###### Note

For more information about using the Amazon S3 Express One Zone storage class with directory buckets, see [S3 Express One Zone](./directory-bucket-high-performance.html#s3-express-one-zone) and [Working with directory buckets](./directory-buckets-overview.html).

###### Important

In the Amazon S3 console, when you choose **Open** or **Download As** for an object, these operations create presigned URLs. For the duration of five minutes, your object will be accessible to anyone who has access to these presigned URLs. For more information about presigned URLs, see [Using presigned URLS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html).

With Amazon S3, you pay only for what you use. For more information about Amazon S3 features and
pricing, see [Amazon S3](https://aws.amazon.com/s3). If you are a new Amazon S3 customer,
you can get started with Amazon S3 for free. For more information, see

[AWS Free Tier](https://aws.amazon.com/free).