# AWS CloudFront

AWS CloudFront is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds. It integrates with other AWS services and provides various features for content distribution and edge caching.

## CloudFront Architecture

AWS CloudFront consists of several key components that work together to deliver content efficiently and securely:

### 1. Distributions
   - **Description:** A CloudFront Distribution is a configuration that specifies how content should be delivered. There are two main types of distributions: Web Distributions and RTMP Distributions.
   - **Architecture:**
     - **Web Distribution:** Used for delivering web content such as HTML, CSS, JavaScript, and images.
     - **RTMP Distribution:** Used for delivering media files using Adobe's RTMP protocol (deprecated).
   - **Use Case:** A company wants to deliver its website's static assets (images, JavaScript, CSS) to users worldwide with low latency. They set up a Web Distribution to cache and serve these assets.
   - **Billing Details:** Charges are based on the data transferred out of CloudFront, the number of requests, and the region from which content is served.
   - **Commands:**
     ```bash
     # Create a CloudFront Distribution using AWS CLI
     aws cloudfront create-distribution --origin-domain-name example.com
     ```

### 2. Origins
   - **Description:** Origins are the source servers where CloudFront fetches the content. Origins can be an S3 bucket, an HTTP server, or an Elastic Load Balancer.
   - **Architecture:**
     - **Amazon S3 Bucket:** Store and serve static content.
     - **HTTP Server:** Any server or web application serving dynamic content.
     - **Elastic Load Balancer (ELB):** Distributes incoming traffic across multiple instances.
   - **Use Case:** An e-commerce site uses an S3 bucket to store product images and a web server to handle user requests. CloudFront fetches images from S3 and dynamic content from the web server.
   - **Billing Details:** Charges for data transferred from the origin to CloudFront and requests made to the origin.
   - **Commands:**
     ```bash
     # Create a CloudFront Distribution with an S3 origin using AWS CLI
     aws cloudfront create-distribution --origin-domain-name mybucket.s3.amazonaws.com --default-root-object index.html
     ```

### 3. Cache Behaviors
   - **Description:** Cache Behaviors define how CloudFront caches content and how it handles requests. You can set up different cache behaviors for different URL paths.
   - **Architecture:**
     - **Path Patterns:** Define how different URL paths are handled (e.g., `/images/*` vs. `/videos/*`).
     - **Caching Policies:** Control cache expiration and invalidation rules.
   - **Use Case:** A news website wants to cache images for a longer duration than news articles. They configure different cache behaviors to handle `/images/*` and `/articles/*` paths with distinct caching rules.
   - **Billing Details:** Charges are based on cache hit/miss ratios and the amount of data transferred.
   - **YAML Code:**
     ```yaml
     # Example of a Cache Behavior configuration
     {
       "PathPattern": "/images/*",
       "TargetOriginId": "S3Origin",
       "ViewerProtocolPolicy": "redirect-to-https",
       "AllowedMethods": ["GET", "HEAD"],
       "CachedMethods": ["GET", "HEAD"],
       "ForwardedValues": {
         "QueryString": false,
         "Cookies": {"Forward": "none"}
       }
     }
     ```

### 4. Edge Locations
   - **Description:** Edge Locations are data centers around the world where CloudFront caches content. They are the geographical locations that deliver content to users.
   - **Architecture:** 
     - **Global Network:** CloudFront has a large network of edge locations spread across various regions to ensure low latency.
   - **Use Case:** A global application needs to ensure that users from different continents experience minimal latency. CloudFront's edge locations cache content closer to users to provide faster load times.
   - **Billing Details:** No direct charges for edge locations; costs are based on data transfer and requests.
   - **Commands:**
     ```bash
     # List CloudFront Edge Locations using AWS CLI
     aws cloudfront list-distributions
     ```

### 5. Origin Groups
   - **Description:** Origin Groups allow you to define multiple origins for a distribution and set up failover capabilities.
   - **Architecture:**
     - **Primary Origin:** The main origin where CloudFront fetches content.
     - **Secondary Origin:** Used for failover if the primary origin becomes unavailable.
   - **Use Case:** A company wants to ensure high availability for its content delivery. They set up an Origin Group with a primary origin (S3 bucket) and a secondary origin (another S3 bucket) to handle failover.
   - **Billing Details:** Costs include data transfer and requests for both primary and secondary origins.
   - **Commands:**
     ```bash
     # Create an Origin Group using AWS CLI
     aws cloudfront create-origin-group --distribution-id <DistributionID> --origin-group-id <OriginGroupID> --origins <PrimaryOrigin> <SecondaryOrigin>
     ```

### 6. SSL/TLS Certificates
   - **Description:** SSL/TLS certificates ensure secure communication between CloudFront and end users. You can use AWS Certificate Manager (ACM) or upload your own certificates.
   - **Architecture:**
     - **AWS Certificate Manager (ACM):** Provides free SSL/TLS certificates for use with CloudFront.
     - **Custom Certificates:** Upload and use your own certificates.
   - **Use Case:** A financial services company requires HTTPS for secure transactions. They use ACM to provision and manage SSL/TLS certificates for their CloudFront distribution.
   - **Billing Details:** Costs associated with SSL/TLS certificates are included in the CloudFront pricing. ACM certificates are free if issued by ACM.
   - **Commands:**
     ```bash
     # Request an SSL/TLS certificate using ACM
     aws acm request-certificate --domain-name example.com --validation-method DNS
     ```

### 7. Web Application Firewall (WAF)
   - **Description:** AWS WAF integrates with CloudFront to protect applications from common web exploits.
   - **Architecture:**
     - **Rules:** Define conditions to allow or block traffic based on IP addresses, HTTP headers, or URL patterns.
     - **Web ACLs:** Associate rules with CloudFront distributions to filter incoming traffic.
   - **Use Case:** An application needs to protect against SQL injection and cross-site scripting attacks. They set up AWS WAF with specific rules and associate it with their CloudFront distribution.
   - **Billing Details:** Charges are based on the number of web ACLs, rules, and requests processed.
   - **Commands:**
     ```bash
     # Create a Web ACL using AWS CLI
     aws wafv2 create-web-acl --name <WebACLName> --scope CLOUDFRONT --default-action Allow
     ```

## Setting Up CloudFront

### Step-by-Step Guide

1. **Create a CloudFront Distribution:**

   - **AWS Management Console:**
     - Go to the CloudFront dashboard.
     - Click on "Create Distribution."
     - Choose the distribution type (Web or RTMP).
     - Configure the origin settings and cache behaviors.
   
   - **AWS CLI:**
     ```bash
     aws cloudfront create-distribution --origin-domain-name example.com
     ```

2. **Configure Origins:**

   - **AWS Management Console:**
     - During distribution creation, specify the origin settings (S3 bucket, HTTP server, etc.).
   
   - **AWS CLI:**
     ```bash
     aws cloudfront create-origin --origin-domain-name mybucket.s3.amazonaws.com
     ```

3. **Set Up Cache Behaviors:**

   - **AWS Management Console:**
     - Define cache behaviors based on URL paths and configure caching policies.
   
   - **AWS CLI:**
     ```bash
     aws cloudfront create-cache-behavior --distribution-id <DistributionID> --path-pattern /images/* --target-origin-id S3Origin
     ```

4. **Configure SSL/TLS Certificates:**

   - **AWS Management Console:**
     - Go to the SSL/TLS settings in the CloudFront distribution.
     - Choose or upload a certificate.
   
   - **AWS CLI:**
     ```bash
     aws acm request-certificate --domain-name example.com --validation-method DNS
     ```

5. **Integrate AWS WAF:**

   - **AWS Management Console:**
     - Create a Web ACL in AWS WAF and associate it with your CloudFront distribution.
   
   - **AWS CLI:**
     ```bash
     aws wafv2 create-web-acl --name <WebACLName> --scope CLOUDFRONT --default-action Allow
     ```

## Billing Details

### Cost Factors

1. **Data Transfer:** Charges for data transferred out of CloudFront to the internet.
2. **Requests:** Costs based on the number of HTTP/HTTPS requests made to CloudFront.
3. **Invalidations:** Charges for invalidating cached content.
4. **SSL/TLS Certificates:** Costs for managing SSL/TLS certificates if not using ACM.
5. **WAF:** Charges for AWS WAF rules and web ACLs if used.

### Pricing Tiers

- **Data Transfer Out:** Costs vary by region. Lower rates apply to higher usage.
- **Requests:** Charged per request type (HTTP or HTTPS).
- **Invalidation Requests:** Charged based on the number of paths invalidated.
- **WAF:** Costs are based on the number of web ACLs and rules.

For detailed and up-to-date pricing information, refer to the [AWS Pricing Calculator](https://calculator.aws/#/) and the [AWS CloudFront Pricing page](https://aws.amazon.com/cloudfront/pricing/).

This README provides a comprehensive overview of AWS CloudFront, including its components, architecture, use cases, billing details, and relevant commands and configurations. It serves as a detailed guide for managing and optimizing CloudFront in AWS environments.
