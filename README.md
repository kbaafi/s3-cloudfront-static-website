[upload]:images/upload.png
[statichost]:images/static.png
[cloudfront]:images/cloudfront.png
[website]:images/website.png
[websitelink]: http://kb-uda-website.s3.amazonaws.com/index.html "http://kb-uda-website.s3.amazonaws.com/index.html"

# Launcing a static website with S3 and CloudFront

This project shows you how to launch a static website using AWS S3 and CloudFront. The webfiles are uploaded to S3 secured and then configured to deliver web content through CloudFront

## Setting up our S3 Bucket

1. Create and S3 bucket and on the (3) Set Permissions tab, uncheck Block all public access. This will allow the files to be accessible from anywhere on the web

2. Upload the files from local system to S3

![upload]

3. **Bucket Policy:** A bucket policy will ensure that web clients are allowed to access the files in the buckets. Under **bucket_name>Permissions**, the following json script is entered into the bucket policy settings:

 ```json
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"AddPerm",
      "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::kb-uda-website/*"]
    }
  ]
}
 ```

4. **Configuring S3 Hosting**: Under **bucket_name>Properties**, select **Static website hosting** and set the index and error page links accordingly

![statichost]

5. **Distribution with CloudFront**

    5.1 Under **AWS CloudFront**, click the Create Distribution button and then **Get Started** under **Web**

    5.2 The following settings are used to configure the website on CloudFront:

    ```yml
    "Origin Domain Name": kb-uda-website.s3.amazonaws.com
    "Origin Path": /
    ```

    Under **Distribution Settings**, I set the *Price Class* to **Use Only U.S, Canada and Europe**

    5.3 Click **Create Distribution** to publish the website

    ![cloudfront]

## The hosted website

The website is hosted at: http://kb-uda-website.s3.amazonaws.com/index.html and is shown below:

![website]
