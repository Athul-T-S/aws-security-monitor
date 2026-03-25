# AWS Real-Time Security Incident Monitoring

A cloud-native security solution that monitors AWS account activity in real-time. It uses **CloudTrail** for logging, **Amazon EventBridge** for threat detection, and **Amazon SNS** for instant email alerting.

## 🛡️ Attacks Detected
This project specifically monitors for high-risk activities, including:
* **Persistence:** Detection of IAM Access Key creation.
* **Privilege Escalation:** Monitoring for 'Attach' or 'Put' policy actions on IAM Users and Roles.
* **Defense Evasion:** Immediate alerts if CloudTrail logging is stopped, deleted, or updated.
* **Data Leakage:** Detection of S3 Bucket Policy or ACL changes.
* **Backdoor Access:** Monitoring for unauthorized Security Group ingress rules.

## 🏗️ Architecture

The flow of data is:
1. **AWS CloudTrail** captures API calls and sign-in events.
2. **Amazon EventBridge** evaluates these events against a custom pattern.
3. If a match is found, **Amazon SNS** triggers an email notification to the administrator.

## 🚀 How to Setup
1. **Create an SNS Topic:** Create a standard SNS topic and subscribe your email address to it.
2. **Enable CloudTrail:** Ensure you have a Trail active in your region.
3. **Create EventBridge Rule:** - Create a new rule in the EventBridge console.
   - Use the `event-pattern.json` file provided in this repo as the **Event Pattern**.
   - Set the **Target** to your SNS Topic.
4. **Test:** Try to create an IAM user or modify a Security Group to receive an instant alert.
