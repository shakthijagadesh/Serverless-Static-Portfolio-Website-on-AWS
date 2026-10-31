# Serverless-Static-Portfolio-Website-on-AWS
A serverless, secure, and low-latency cloud portfolio hosted on Amazon Web Services (AWS) using Amazon S3, Amazon CloudFront, and Origin Access Control (OAC) .

# Architecture Overview

[ Visitor Browser ] 
        ──>
        
[ Amazon CloudFront CDN ]  
        ──>
        
[ Private Amazon S3 Bucket ] 

1.Amazon S3: Stores static site assets (index.html) in a private bucket with Block Public Access fully enabled.

2.Amazon CloudFront: Acts as a Content Delivery Network (CDN) distributing assets across global edge locations with automatic SSL/TLS encryption.

3.Origin Access Control (OAC): Secures communication between CloudFront and S3 using AWS Signature Version 4 (SigV4), preventing any direct access to the storage bucket.

4.Least-Privilege Bucket Policy: An IAM bucket policy restricts read permissions (s3:GetObject) strictly to the CloudFront distribution ARN, mitigating confused deputy risks.


*Key Security Features

1.Zero Direct Public S3 Access: The S3 bucket rejects all non-CloudFront requests, preventing data exposure.

2.Confused Deputy Prevention: The AWS:SourceArn condition in the S3 bucket policy ensures that only this specific distribution can query the bucket.

3.HTTPS Enforcement: CloudFront automatically upgrades all incoming insecure HTTP traffic to HTTPS (port 443).

4.Cost Efficiency: Serverless architecture with zero compute overhead or idle instance costs.

* Deployment Steps
  
1.Storage Setup: Created S3 bucket shakthi-portfolio-site-2026 with private access.

2.File Upload: Uploaded production index.html.

3.CDN Creation: Configured CloudFront distribution pointing to S3 origin with OAC authentication.

4.Policy Enforcement: Attached the generated OAC JSON bucket policy to S3.

5.Edge Cache Management: Applied cache invalidation paths (/*) for immediate updates.

