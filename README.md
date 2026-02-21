# A SECURITY MONITORING TOOL TO SAFEGUARD SECRETS IN AWS
Stage 1: Secret & Logging

Step 1: In this project, I will demonstrate how to store sensitive data securely using AWS Secrets Manager. I’m doing this project to learn how cloud environments protect credentials and prevent hard-coding secrets.

Step 2: In this project, I will demonstrate how to enable CloudTrail to log account activity. I’m doing this project to learn how security teams track and audit actions in AWS.

Step 3: In this project, I will demonstrate how to test CloudTrail by accessing my secret and verifying the log entry. I’m doing this project to understand how actions leave audit trails.

Stage 2: Monitoring & Alerts

Step 4: In this project, I will demonstrate how to create a CloudWatch log filter for secret access events. I’m doing this project to learn how to detect sensitive activity.

Step 5: In this project, I will demonstrate how to configure a CloudWatch Alarm and SNS email alert. I’m doing this project to learn real-time

Tools and concepts
Services I used were AWS Secrets Manager for securely storing and retrieving sensitive data, AWS CloudTrail for tracking API activity and account actions, Amazon CloudWatch for log analysis, metrics, and alarms, and Amazon Simple Notification Service for sending real-time email notifications.

Key concepts I learnt include secure secret management, audit logging, log forwarding, metric filters, alarm thresholds, evaluation periods, and the importance of choosing the correct statistic (such as Sum vs Average) when configuring alarms. I also learnt how to design an end-to-end monitoring pipeline — from detecting an event, to converting it into a metric, to triggering an alert — which is a core skill in cloud security and incident detection.

