📊 AWS CloudWatch Dashboards for Comprehensive Monitoring


---

✅ Overview of Your 4 Dashboards:

## ✅ CloudWatch Dashboard Summary

| Area                        | Dashboard Name                | Status from Screenshot                            |
|-----------------------------|-------------------------------|----------------------------------------------------|
| Billing & Cost              | `Billing_Cost`                | ✅ Complete (widgets showing data)                |
| Application & System Logs   | `Logs_Dashboard`              | ⚠ Error in queries (Log Insights issue)           |
| Network Performance         | `Network_Performance_Dashboard` | ✅ Metrics exist (some empty)                    |
| Security & Compliance       | `Security_Compliance_Dashboard` | ✅ Working fine                                  |




---

🔹 Step-by-Step Setup Guide

1. Billing and Cost Dashboard

🎯 Goal:

Daily estimated charges

Monthly breakdown

Charges by service (EC2, S3)


🔧 Steps:

1. Enable CloudWatch Billing Alerts
Go to: Billing Preferences → Enable “CloudWatch billing alerts”.


2. Go to CloudWatch → Dashboards → Create Dashboard → Billing_Cost


3. Add Widgets:

📊 Bar Chart:
Metrics:

AWS/Billing → EstimatedCharges (USD)
Filter by ServiceName = EC2, S3

🔢 Number Widget:
Shows total EstimatedCharges this month

![Image](https://github.com/user-attachments/assets/64617908-9a3c-4ba1-bc97-0a511c7a8b30)
---

2. Logs Dashboard

🎯 Goal:

Show errors/exceptions, response times, failed logins


🛠 Problem: Your current query has syntax errors.

🔧 Fix & Steps:

1. Ensure logs are sent to CloudWatch:

Agent installed ✔ (verified in your EC2 terminal)

Config file valid ✔

Logs from /var/log/messages, etc. enabled ✔



2. Go to CloudWatch → Logs Insights → Choose log group


3. Sample Queries:

🔴 Errors & Exceptions:

fields @timestamp, @message
| filter @message like /error/i
| sort @timestamp desc
| limit 20

⏱ Response Times:

fields @timestamp, latency, status
| sort latency desc
| limit 10

❌ Failed Logins:

fields @timestamp, @message
| filter @message like /Failed password/


4. Save queries → Add to dashboard (Logs_Dashboard)
Choose graph/table view as needed.

![Image](https://github.com/user-attachments/assets/251c632f-0803-410b-b34f-2ca6d57295d2)
---

3. Network Performance Dashboard

🎯 Goal:

Monitor VPC, EC2, ELB, CloudFront traffic


🔧 Steps:

1. Dashboard: Network_Performance_Dashboard


2. Widgets to Add:

📈 EC2 Metrics:

Metric: NetworkIn and NetworkOut

Namespace: AWS/EC2


⚠ Load Balancer Errors:

HTTPCode_ELB_5XX_Count, RequestCount

Namespace: AWS/ApplicationELB or AWS/ELB


🌐 CloudFront Usage:

BytesDownloaded, BytesUploaded

Namespace: AWS/CloudFront




3. Use line charts for trend clarity.

![Image](https://github.com/user-attachments/assets/3f64da2f-73e2-4baa-90ac-d8931fc48731)---

4. Security & Compliance Dashboard

🎯 Goal:

Monitor AWS security services


🔧 Steps:

1. Dashboard: Security_Compliance_Dashboard


2. Widgets to Add:

✅ GuardDuty findings:

Namespace: AWS/GuardDuty

Metric: FindingCount, filtered by severity


🛡 AWS Config Non-compliant Resources

Metric: Compliance


🔐 CloudTrail Events:

Use Log Insights or custom queries

For API activity, unauthorized attempts


🔑 IAM Access Key Usage or Console login
Example query for failed logins:

fields eventName, userIdentity.userName, errorCode
| filter eventName = "ConsoleLogin" and errorMessage like /failed/i



3. Use table widgets for logs and gauges for counts.

![Image](https://github.com/user-attachments/assets/291d557a-c83f-4623-b487-de155611c385)---
