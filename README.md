# aws-static-portfolio-s3-cloudfront
Infrastructure documentation for hosting a static portfolio website on AWS using S3, CloudFront, and IAM.o

## Architecture Overview
This project hosts a static HTML portfolio on Amazon S3 and serves it globally using Amazon CloudFront. CloudFront is the only public entry point, while S3 acts as the origin.

## AWS Services Used
- Amazon S3 – static website hosting
- Amazon CloudFront – CDN and HTTPS termination
- AWS IAM – user separation and MFA
- AWS Route 53 – domain and DNS (in progress)
- AWS Certificate Manager (ACM) – TLS certificate (in progress)

## Request Flow
Browser → CloudFront (edge location) → S3 origin bucket

## Key Design Decisions
- CloudFront is the public-facing layer, not S3
- IAM users are separated by role (admin vs upload)
- MFA enforced on privileged access
- Cache invalidation used intentionally to control updates

## Cache Invalidation Notes
When updating `index.html`, CloudFront may continue serving cached content.
Invalidations are used for:
- `/index.html`
- `/`

## Security Considerations
- No AWS credentials stored in the front-end
- Least privilege IAM policies
- S3 bucket access restricted to CloudFront
- TLS termination handled at CloudFront

## Lessons Learned
- CloudFront caching behavior and invalidation timing
- The importance of separating identity roles
- How DNS, HTTPS, and CDN layers work together

## Next Improvements
- Complete Route 53 + ACM setup for custom domain
- Add diagrams and screenshots
- Explore Origin Access Control (OAC)
