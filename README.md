🌐 Static Website Hosting on AWS (S3 + CloudFront + Route 53 + ACM)

This project demonstrates how to deploy a static website on Amazon Web Services (AWS) using a cost-effective, serverless, and highly available architecture. It leverages Amazon S3 for hosting the content, CloudFront for global content delivery, ACM for HTTPS, and Route 53 for custom domain DNS management.
📐 Architecture Overview
✅ Amazon S3

    Configured for static website hosting

    Stores static files such as HTML, CSS, JS, and images

✅ CloudFront (CDN)

    Delivers cached content globally for low latency

    Uses an Origin Access Identity (OAI) to securely access S3

    Redirects HTTP traffic to HTTPS

✅ AWS Certificate Manager (ACM)

    Provides a free public SSL/TLS certificate

    Certificate issued in the us-east-1 (N. Virginia) region to support CloudFront

✅ Amazon Route 53

    Used to configure custom domain DNS

    Maps the domain (e.g., yourdomain.com) to the CloudFront distribution

    Hosted zone contains A (Alias) records pointing to CloudFront

🚀 Deployment Instructions
🔧 1. Set Up the ACM Certificate (us-east-1)

    Request a public SSL certificate in N. Virginia (us-east-1)

    Add DNS validation records via Route 53

    Ensure certificate status is ISSUED before proceeding

📂 2. Prepare and Upload Website Content

    Create your static site (index.html, styles.css, etc.)

    Upload files to your S3 bucket using:

    aws s3 sync ./site-files s3://your-bucket-name

📄 3. Deploy the Infrastructure via CloudFormation

    Use the static-site.yaml template provided

    Parameters required:

        DomainName: Your full domain (e.g., example.com)

        HostedZoneId: Your Route 53 Hosted Zone ID

        CertificateArn: ACM certificate ARN from us-east-1

Deploy via AWS Console or CLI:

aws cloudformation create-stack \
  --template-body file://static-site.yaml \
  --stack-name StaticSite \
  --parameters ParameterKey=DomainName,ParameterValue=example.com \
               ParameterKey=HostedZoneId,ParameterValue=Zxxxxxxxxxxxx \
               ParameterKey=CertificateArn,ParameterValue=arn:aws:acm:us-east-1:xxxx:certificate/xxxxxx \
  --capabilities CAPABILITY_NAMED_IAM

🔁 4. Validate Deployment

    Confirm:

        S3 bucket is created

        CloudFront distribution is deployed and configured

        DNS alias record in Route 53 points to CloudFront

    Open your browser and visit:
    https://yourdomain.com

🧪 Lessons Learned

    Importance of issuing ACM certificates in us-east-1 for CloudFront

    Ensuring DNS validation is complete before using ACM certs

    Proper use of Origin Access Identity for S3 security

    Handling S3 Block Public Access settings when configuring bucket policies

📁 Repository Structure

aws-static-site/
├── site-files/                 # Your HTML/CSS/JS files
│   └── index.html
├── static-site.yaml           # CloudFormation template
├── architecture-diagram.png   # System architecture (optional)
└── README.md

📜 Contributors and References

    AWS Documentation

    AWS Community forums & StackOverflow

✨ Conclusion

This project showcases how to deploy a fully serverless, secure, and globally accessible static website on AWS. It's a reliable, cost-effective solution for personal websites, portfolios, and documentation pages. It can be further enhanced with CI/CD and WAF integration.

Feel free to contribute, suggest improvements, or raise issues!
