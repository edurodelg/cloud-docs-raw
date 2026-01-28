---
source_url: https://docs.aws.amazon.com/AmazonS3/latest/userguide/transfer-acceleration-speed-comparison.html
fetched_at: 2026-01-28T07:12:42.591806
---

# Using the Amazon S3 Transfer Acceleration
        Speed Comparison tool

# Using the Amazon S3 Transfer Acceleration Speed Comparison tool

You can use the [Amazon S3 Transfer Acceleration Speed Comparison tool](https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html) to compare accelerated and
non-accelerated upload speeds across Amazon S3 Regions. The Speed Comparison tool uses multipart
uploads to transfer a file from your browser to various Amazon S3 Regions with and without using
Transfer Acceleration.

You can access the Speed Comparison tool by using either of the following methods:

-
Copy the following URL into your browser window, replacing


with the AWS Region that you are using (for example,`region`

`us-west-2`

) and

with the name of the bucket that you want to evaluate:`amzn-s3-demo-bucket`

`https://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html?region=`

`region`

&origBucketName=`amzn-s3-demo-bucket`

For a list of the Regions supported by Amazon S3, see

[Amazon S3 endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/s3.html)in the*AWS General Reference*. -
Use the Amazon S3 console.