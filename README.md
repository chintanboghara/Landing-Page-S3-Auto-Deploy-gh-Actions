# Hey Beast Landing Page Deployment

This repository contains the landing page for Hey Beast, automatically deployed to an AWS S3 bucket using GitHub Actions. The deployed site is accessible at [http://hey-beast-landing-page.s3-website.ap-south-1.amazonaws.com](http://hey-beast-landing-page.s3-website.ap-south-1.amazonaws.com).

## Deployment

The deployment is managed by a GitHub Actions workflow defined in `.github/workflows/main.yml`. It triggers on pushes to the `main` branch and includes the following steps:

1. **Checkout the repository**: Retrieves the latest code using `actions/checkout@v1`.
2. **Configure AWS Credentials**: Authenticates with AWS using secrets stored in GitHub.
3. **Deploy to S3**: Syncs the repository files to the `hey-beast-landing-page` S3 bucket with the `--delete` flag to remove outdated files.

For more details, refer to the [workflow file](.github/workflows/main.yml).

## Prerequisites

- An AWS account with an S3 bucket (`hey-beast-landing-page`) configured for static website hosting. See [AWS S3 documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) for setup instructions.
- AWS credentials (`AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`) stored as secrets in your GitHub repository. Learn how to configure secrets in the [GitHub documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets).

## AWS S3 Bucket Configuration

To host the static website, configure your S3 bucket as follows:

1. Navigate to your S3 bucket in the AWS Management Console.
2. Go to the **Properties** tab.
3. Enable **Static website hosting** under that section.
4. Set the index document to `index.html` and optionally specify an error document.

For detailed guidance, consult the [AWS S3 documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html).

## Public Access Policy

The `hey-beast-landing-page` bucket is set to allow public read access, enabling the static website to be publicly accessible. The bucket policy is:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::hey-beast-landing-page/*"
        }
    ]
}
```

**Note:** Public access means anyone can view the bucket's files. Verify this meets your security needs and avoid storing sensitive data in the bucket.
