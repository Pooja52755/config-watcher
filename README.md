🚀 ConfigWatcher: Automated Multi-Environment Configuration Drift Detection
🔍 Project Overview
Modern cloud-native applications often span multiple environments—development, staging, and production. But ensuring consistent configuration across these environments is challenging. Manual validation is error-prone, leading to silent bugs, deployment failures, and unexpected behavior.

ConfigWatcher solves this problem.

It is a lightweight, fully serverless solution that proactively identifies and reports .env configuration drifts between environments—before they cause issues. Built using core AWS services, ConfigWatcher continuously monitors environment files stored in Amazon S3, performs smart comparisons, and sends clear, actionable drift reports via Amazon SES—all without human intervention.

✨ Key Features
🔁 Automated Monitoring
Automatically retrieves .env files (local.env, staging.env, production.env) from a designated S3 bucket.

🧠 Intelligent Drift Detection
Compares key-value pairs and flags mismatches or missing keys across environments.

📋 Comprehensive Drift Reports
Generates detailed, structured reports outlining all configuration discrepancies.

📧 Actionable Email Alerts
Sends both HTML and plain-text reports directly to your inbox via Amazon SES for maximum readability and visibility.

🧹 Clean, Human-Readable Output
Avoids raw dumps—emails are clean, styled, and professional.

🛠️ AWS Services Used
Service	Role
AWS Lambda	Executes drift detection and sends email reports
Amazon S3	Stores .env files securely across different environments
Amazon SES	Sends email alerts with high deliverability
AWS IAM	Manages permissions for Lambda to access S3 and SES securely
CloudWatch / EventBridge	(Optional) Schedules Lambda to run periodically

⚙️ How It Works (Behind the Scenes)
✅ 1. Scheduled Trigger
CloudWatch/EventBridge triggers the Lambda function on a predefined schedule (e.g., daily or hourly).

📂 2. Retrieve Configurations
Lambda connects to Amazon S3.

Downloads local.env, staging.env, production.env.

Parses and converts them into Python dictionaries using the parse_env helper function.

🕵️‍♂️ 3. Drift Detection Logic
Compares all keys and values across the three environments.

Flags:

❌ Missing Keys

🔁 Mismatched Values

Compiles results into a drift report list.

✉️ 4. Report Generation
Constructs:

✅ A plain-text email for all clients.

🌐 An HTML email (styled table, clean layout).

Subject line reflects severity (e.g., 🔥 Drift Detected: 3 Issues).

📤 5. Email Notification (Amazon SES)
Lambda uses Amazon SES to send the report.

Works even in sandbox mode (when both sender & receiver are verified).

Confirms with Message ID on success.

🧪 Sample Email Output (HTML)
html
Copy
Edit
Subject: 🚨 Config Drift Detected Between Environments

Hi Team,

Here is your latest config drift report:

| Key            | local.env     | staging.env   | production.env |
|----------------|---------------|---------------|----------------|
| DB_HOST        | localhost     | staging-db    | production-db  |
| PAYMENT_API_KEY| ❌ MISSING    | sk_test_123   | sk_test_456    |
| TIMEOUT        | 3000          | 5000          | 5000           |

✔ Please review the discrepancies and align the environments accordingly.
🚀 Deployment Steps
AWS Account Setup

Ensure you have an active AWS account.

S3 Bucket

Create a bucket (e.g., configwatcher-envs) and upload your .env files.

SES Setup

Verify sender & receiver emails (e.g., harshitapoojaande@gmail.com & ande.harshitapooja@gmail.com) in the same AWS region.

Lambda Function

Runtime: Python 3.x

Upload lambda_function.py

Use IAM Role (ConfigWatcherLambda-role) with:

s3:GetObject on arn:aws:s3:::configwatcher-envs/*

ses:SendEmail on your verified SES identity

CloudWatch logs permissions

Schedule with CloudWatch

Set up a cron rule to trigger the function (e.g., every 24 hours).

🎬 Demo Video
🎥 A short, impactful video walk-through (Coming Soon!):

✅ Overview of the problem (config drift)

⚙️ Step-by-step walk-through of the Lambda code

💡 S3 bucket preview with sample .env files

🧪 Manual Lambda trigger

📥 Live receipt of a beautifully formatted email

🛠️ Simulating a config change and showing the updated drift report

[🔗 YouTube / Vimeo Link Placeholder]

💡 Why ConfigWatcher Matters
Problem	                    Solution with ConfigWatcher
Silent config mismatches	  Auto-detection and reporting
Manual drift checks	        Fully automated serverless monitoring
Delayed bug discovery	      Proactive alerts prevent late surprises
Poorly formatted emails	    Clean, styled, professional reports
Resource-heavy solutions	  Lightweight, Free Tier-friendly setup
