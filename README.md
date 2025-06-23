🚀 ConfigWatcher
Automated Multi-Environment Configuration Drift Detection

🧠 Problem Statement
In cloud-native development, even a small difference between .env files across environments (local, staging, production) can break deployments or introduce bugs.

Manual checks are tedious, error-prone, and unscalable.

💡 Solution: ConfigWatcher
ConfigWatcher is a serverless drift detection tool that monitors .env files across environments and automatically alerts you when any mismatch is found. It is lightweight, cloud-native, and runs entirely on AWS.

🔍 What It Does

✅ Detects mismatches or missing keys in .env files

✅ Compares local.env, staging.env, and production.env

📬 Sends easy-to-read reports directly to your inbox

⚡ Runs automatically when you upload new config files (via S3 trigger)

✨ Key Features

✅ S3 Event Trigger: Runs automatically when new .env files are uploaded

✅ AWS Lambda Powered: Handles parsing, comparison, and emailing

✅ Smart Drift Detection: Highlights missing keys and mismatched values

✅ Email Reports via SES: Clean HTML + plain-text summaries

✅ No UI Needed: All insights delivered via email

✅ Free Tier Friendly: Perfect for startups or small teams

🛠️ AWS Architecture
Service	Purpose
🧠 AWS Lambda	Detects drift and sends report
📁 Amazon S3	Stores uploaded .env files
📤 Amazon SES	Sends alert emails to your inbox
🔒 AWS IAM	Secure access between services
🟢 S3 Event	Triggers Lambda on file upload
📊 CloudWatch	Logs Lambda activity

⚙️ How It Works

A[S3: .env File Uploaded] --> B[Trigger AWS Lambda]
B --> C[Fetch all .env Files from S3]
C --> D[Compare Keys & Values]
D --> E[Generate Drift Report]
E --> F[Send Report via SES]
F --> G[Inbox: Drift Alert 🚨]

📧 Email Setup for Judges (in README.md)

## 🧪 Testing Email Alerts (Important Note for Judges)

By default, AWS SES only allows sending emails to **verified addresses** when in sandbox mode.

To test the email functionality of ConfigWatcher:

1. Open `lambda_function.py`
2. Go to the section:
   ```python
   Source='harshitapoojaande@gmail.com',
   Destination={'ToAddresses': ['ande.harshitapooja@gmail.com']},
Replace both emails with your own verified email addresses in SES (or remove SES code to skip email sending).

Deploy the function and upload .env files to the S3 bucket.

Subject: 🚨 ConfigWatcher: Drift Detected in Production Config

🚀 Why It Matters

⏱ Saves hours of debugging

🛡 Prevents deployment failures

📣 Gives DevOps real-time visibility

🧪 Perfect for CI/CD pipelines

🧪 Demo Steps

Upload .env files to S3 bucket

Lambda gets triggered automatically

Configs are compared

Email sent if drift is detected

Upload new configs → Get updated drift status

🎥 Demo Video Link – https://vimeo.com/1095505331?share=copy

📦 Deploy in Minutes
S3: Upload .env files to your bucket

SES: Verify sender & receiver emails

Lambda: Deploy function with lambda_function.py

IAM: Attach permissions for S3, SES, and logs

S3 Trigger: Enable on PUT event for .env uploads

🌟 What Makes It Special
🔁 Auto-Healing Watchdog for configs

✨ Zero UI – all in your inbox

💸 Runs on AWS Free Tier

⚡ Built for real-world DevOps use, not just for show

🧠 Hackathon Takeaway
ConfigWatcher turns a boring task into a clean, powerful automation. It’s not just a tool—it’s DevOps best practices, automated.
