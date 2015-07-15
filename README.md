Static website to generate directory listing for S3 buckets.

## Usage
Clone the repository and edit [config.js](https://github.com/sgtFloyd/s3-autoindex/blob/master/config/config.js), configuring it with your bucket.
- Set `window.S3_BUCKET_URL` to bucket's REST endpoint.
- Alternatively, set `window.SECRET_BUCKET_URL` to your AES-encrypted REST endpoint for a password-protected directory listing. You'll need to enter your encryption key before the page will load.

**Note:** The S3 REST endpoint used differs from S3's website endpoint. For more details, see: [Website Rest EndpointDiff](http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteEndpoints.html#WebsiteRestEndpointDiff).

#### S3 Bucket Permissions
You must setup the S3 website bucket to allow public read access.

* Grant `Everyone` the `List` and `View` permissions:
![](http://s3.sgtfloyd.com/img/s3_management_console.png)

* Assign the following Bucket Policy:
```
{
    "Version": "2008-10-17",
    "Statement": [
        {
            "Sid": "AllowPublicRead",
            "Effect": "Allow",
            "Principal": {
                "AWS": "*"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::{your-bucket-name}/*"
        }
    ]
}
```

* Assign the following CORS Configuration:
```
<CORSConfiguration>
 <CORSRule>
   <AllowedOrigin>*</AllowedOrigin>
   <AllowedMethod>GET</AllowedMethod>
   <AllowedHeader>*</AllowedHeader>
 </CORSRule>
</CORSConfiguration>
```
