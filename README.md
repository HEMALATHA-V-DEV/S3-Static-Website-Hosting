# S3-Static-Website-Hosting on Amazon S3 

## 1. Upload files to s3

**a. Clone GitHub Repository:**

Clone Your GitHub Repository:
```bash
git clone https://github.com/<username>/<repo>.git](https://github.com/HEMALATHA-V-DEV/S3-Static-Website-Hosting.git
```

**b. Upload Files to S3:**

- Sign in to AWS Management Console -> Open S3 Service:
- Navigate to the S3 service -> Create a New S3 Bucket - Click “Create bucket.” - Click “Upload.” ( Add your HTML and CSS files )

**Configure Static Website Hosting:**

- Go to the “Properties” tab of the bucket.
- Scroll down to “Static website hosting.”
- Enable “Static website hosting” and specify index.html as the index document.
- Click “Save changes.”

**Set Permissions:**

- Go to the “Permissions” tab.
- Click “Bucket Policy - Add a policy to allow public read access

# 2. Set Up Route 53

**a. Using Existing Domain -> Open Route 53 - Navigate to the Route 53 service in the AWS Management Console.**

- Create a Hosted Zone: - Click “Hosted zones.” - Click “Create hosted zone.” [(e.g., example.com). ]

**b. Create DNS Records:**

- Add A Record for S3 Website: -> In the hosted zone, click “Create record.” 
- Select “Alias” and choose the S3 bucket endpoint from the dropdown (e.g., your-bucket-name.s3-website-us-west-1.amazonaws.com). - Click “Create records.”
- Add CNAME Record for CloudFront ( This step will be done later when configuring CloudFront)
  
## 3. Set Up CloudFront
   
**a. Create a CloudFront Distribution - Open CloudFront - Create a Distribution - Configure Distribution Settings:**

- Origin Domain Name: Choose your S3 bucket from the dropdown.
- Viewer Protocol Policy: Choose “Redirect HTTP to HTTPS” or “HTTPS Only.”
- Alternate Domain Names (CNAMEs): Enter your custom domain (e.g., www.example.com).
- SSL Certificate: Choose “Custom SSL Certificate” and select the certificate for your domain.
You need to have an SSL certificate for your domain from AWS Certificate Manager (ACM).
- Default Root Object: Enter index.html -> Create Distribution:

**b. Update DNS Records:**

- After the distribution is created, note the CloudFront domain name (e.g., d1234abcd8.cloudfront.net).
- Add CNAME Record in Route 53 - Go to your Route 53 hosted zone - Click “Create record.”
Choose “Simple” routing and click “Next.”
For Record name, enter the subdomain (e.g., www).
For Record type, choose CNAME – Canonical name.
For Value, enter the CloudFront distribution domain name (e.g., d1234abcd8.cloudfront.net).
Click “Create records.”

## 4. Verify and Test
Wait for Propagation: DNS changes can take some time to propagate.

**Test Your Website:**

Visit your domain (e.g., http://www.example.com) to verify that the static website is being served correctly.

**Summary**
- Upload to S3: Upload your static website files to an S3 bucket and configure it for static website hosting.
- Set Up Route 53: Create a hosted zone, add DNS records for S3 and CloudFront.
- Configure CloudFront: Create a CloudFront distribution for your S3 bucket, and update Route 53 records to point to CloudFront.
- Verify: Test your website to ensure it’s accessible through your custom domain.
- This process will enable you to serve your static website via a custom domain using Amazon S3, Route 53, and CloudFront.



