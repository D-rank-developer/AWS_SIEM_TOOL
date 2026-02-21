<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Security Monitoring System

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-security-monitoring)

**Author:** Dumanyie Chamberlain  
**Email:** dumanyiechamberlain@gmail.com

---

![Image](http://learn.nextwork.org/sparkling_blue_joyful_nopal/uploads/aws-security-monitoring_reghtjy)

---

## Introducing Today's Project!

Stage 1: Secret & Logging

Step 1:
In this project, I will demonstrate how to store sensitive data securely using AWS Secrets Manager.
I’m doing this project to learn how cloud environments protect credentials and prevent hard-coding secrets.

Step 2:
In this project, I will demonstrate how to enable CloudTrail to log account activity.
I’m doing this project to learn how security teams track and audit actions in AWS.

Step 3:
In this project, I will demonstrate how to test CloudTrail by accessing my secret and verifying the log entry.
I’m doing this project to understand how actions leave audit trails.

Stage 2: Monitoring & Alerts

Step 4:
In this project, I will demonstrate how to create a CloudWatch log filter for secret access events.
I’m doing this project to learn how to detect sensitive activity.

Step 5:
In this project, I will demonstrate how to configure a CloudWatch Alarm and SNS email alert.
I’m doing this project to learn real-time

### Tools and concepts

Services I used were AWS Secrets Manager for securely storing and retrieving sensitive data, AWS CloudTrail for tracking API activity and account actions, Amazon CloudWatch for log analysis, metrics, and alarms, and Amazon Simple Notification Service for sending real-time email notifications.

Key concepts I learnt include secure secret management, audit logging, log forwarding, metric filters, alarm thresholds, evaluation periods, and the importance of choosing the correct statistic (such as Sum vs Average) when configuring alarms. I also learnt how to design an end-to-end monitoring pipeline — from detecting an event, to converting it into a metric, to triggering an alert — which is a core skill in cloud security and incident detection.

### Project reflection

This project took me approximately several hours to complete, including configuration, testing, and troubleshooting each stage of the monitoring pipeline.

The most challenging part was troubleshooting why the alarm was not triggering an email, especially identifying that the statistic needed to be set to Sum instead of Average in Amazon CloudWatch.

It was most rewarding to see the full monitoring system work end-to-end — from retrieving a secret in AWS Secrets Manager, to seeing the alarm activate, and finally receiving the email notification through Amazon Simple Notification Service. That confirmed the security monitoring setup was functioning correctly.

---

## Create a Secret

Secrets Manager is a secure AWS service that allows me to safely store and manage sensitive information such as passwords, API keys, tokens, and credentials instead of exposing them in source code or insecure channels.

You could use Secrets Manager to securely store database credentials, API authentication keys, SSH private keys, or application secrets, automatically rotate them, and monitor access to detect any suspicious or unauthorised activity before it becomes a security incident.

To support the secure configuration of the project, I created a secret named TopSecretInfo. This secret stores sensitive configuration data required by the application at runtime, ensuring that confidential values are not hardcoded in the source code or exposed in version control.

![Image](http://learn.nextwork.org/sparkling_blue_joyful_nopal/uploads/aws-security-monitoring_o5p6q7r8)

---

## Set Up CloudTrail

CloudTrail is a monitoring and auditing service in AWS CloudTrail that records activity and API calls made within an AWS account. It provides visibility into actions such as creating resources, modifying configurations, and accessing sensitive services.

I set up a trail to define exactly which account activities should be recorded and to specify where those logs will be stored, ensuring that all relevant events are captured and saved in a designated Amazon S3 bucket for monitoring, compliance, and security investigation purposes.

CloudTrail events include several types, each providing a different level of visibility into what is happening inside your AWS account:
Management events: These record administrative actions that configure or modify AWS resources, such as creating an EC2 instance, updating IAM policies, or accessing a secret in AWS Secrets Manager. In this project, these events are important because secret access is logged here.

Data events: These capture high-volume operations performed on resources rather than configuration changes. Examples include uploading or downloading objects from Amazon S3 or invoking an AWS Lambda function. 

Insights events: These identify unusual activity patterns in management events, such as a sudden spike in API calls or abnormal IAM activity. 

Network activity events: These monitor network-related operations, including changes to VPC configurations, routing tables, or traffic-related settings.

### Read vs Write Activity

Read API activity involves actions where a user or service views information without making any changes. This includes operations such as listing Amazon S3 buckets, describing Amazon EC2 instances, or viewing metadata about a secret stored in AWS Secrets Manager.

Write API activity involves actions that create, modify, or delete resources. It also includes sensitive operations such as retrieving the actual value of a secret, since this is considered a state-changing or security-impacting action.

For this project, we need to monitor Write API activity in AWS CloudTrail to ensure that any attempt to retrieve or modify a secret is properly logged for auditing and security monitoring purposes.

---

## Verifying CloudTrail

I retrieved the secret in two ways:
First through the AWS Management Console, where I opened AWS Secrets Manager and viewed the stored secret directly from the dashboard interface.
Second using the AWS CLI via AWS CloudShell, where I ran the aws secretsmanager get-secret-value command to programmatically fetch the secret.
This confirmed that the secret can be securely accessed both through the web interface and through the command line, and that the access activity can be monitored in CloudTrail.

To analyse my CloudTrail events, I visited the Event history section in AWS CloudTrail and filtered the Event source by entering secretsmanager.amazonaws.com.

I found several events related to AWS Secrets Manager, including GetSecretValue, GetResourcePolicy, and DescribeSecret. I specifically noticed the GetSecretValue event under my username, which shows the exact time the action occurred and the secret involved.

This tells me that the secret’s value was successfully retrieved from Secrets Manager. In other words, someone (in this case, my account) accessed or used the stored secret. That confirms that CloudTrail is properly logging secret access activity — which is exactly what we want for monitoring and security auditing.

![Image](http://learn.nextwork.org/sparkling_blue_joyful_nopal/uploads/aws-security-monitoring_s8t9u0v1)

---

## CloudWatch Metrics

Amazon CloudWatch Logs is a centralized log management service that collects, stores, and monitors logs from multiple sources across your infrastructure — including applications, servers, network components, and other AWS services.

It’s important for monitoring because it allows you to analyse activity in near real time, detect unusual behaviour, troubleshoot issues quickly, and create metric filters and alarms that trigger notifications when specific events occur. Instead of manually checking logs, CloudWatch helps automate visibility and response — which is essential for maintaining security, performance, and reliability.

The key difference is their purpose and how you use the data.

AWS CloudTrail is focused on recording API activity and account-level actions — basically who did what, when, and from where in your AWS account.

Amazon CloudWatch Logs is focused on monitoring, analysing, and reacting to log data in near real time.

So:

CloudTrail’s Event History is useful for investigating past management events, auditing account activity, and performing security reviews within the last 90 days.

CloudWatch Logs are better for continuously monitoring logs, creating metric filters, setting alarms, and triggering automated alerts when specific actions (like GetSecretValue) occur.

In simple terms:
CloudTrail records the activity.
CloudWatch helps you monitor and respond to it.

A Amazon CloudWatch metric is a numerical time-based measurement that represents activity or performance within your environment. It turns log events into data points that can be graphed, analysed, and used to trigger alarms.

When setting up a metric, the metric value represents the number that is recorded each time the filter detects a matching log event. In this case, setting it to 1 means every time a GetSecretValue action appears in the logs, the counter increases by one — clearly tracking each secret access.

The default value is used when no matching log events are found during a given time period. Setting it to 0 ensures that periods with no secret access are still recorded on the graph, giving a complete and accurate view of activity over time.

![Image](http://learn.nextwork.org/sparkling_blue_joyful_nopal/uploads/aws-security-monitoring_a9b0c1d2)

---

## CloudWatch Alarm

A Amazon CloudWatch alarm is a monitoring feature that watches a specific metric and automatically takes action — such as sending a notification — when that metric crosses a defined threshold.

I set my CloudWatch alarm threshold to greater than or equal to 1 within a 5-minute period so the alarm will trigger whenever the SecretIsAccessed metric records at least one access during that timeframe. This ensures I am immediately alerted any time the secret is retrieved, making it highly effective for security-sensitive monitoring.

Amazon Simple Notification Service (SNS) is a fully managed messaging service that enables you to send notifications from one source to multiple subscribers through a central topic.

I created an SNS topic along the way. An SNS topic is a communication channel that receives messages from services like Amazon CloudWatch and distributes those messages to all subscribed endpoints, such as email addresses, SMS numbers, or other AWS services.

My SNS topic is set up to receive alarm notifications from CloudWatch and forward them to my subscribed email address so that I am immediately alerted whenever my secret is accessed.

AWS requires email confirmation because Amazon Simple Notification Service needs to verify that the email address owner actually agreed to receive notifications. This ensures that alerts are only sent to valid and authorised recipients.

This helps prevent spam, accidental subscriptions, and misuse of notification systems. It also protects users from being unknowingly subscribed to alerts they did not request, maintaining both security and privacy.

![Image](http://learn.nextwork.org/sparkling_blue_joyful_nopal/uploads/aws-security-monitoring_fsdghstt)

---

## Troubleshooting Notification Errors

To test my monitoring system, I retrieved the secret value again from AWS Secrets Manager to generate a GetSecretValue event and trigger the SecretIsAccessed metric in Amazon CloudWatch.

The results were that I did not receive an email notification from Amazon Simple Notification Service, indicating that one part of the monitoring pipeline — either the metric filter, alarm configuration, or SNS subscription — requires further troubleshooting.

When troubleshooting the notification issues, I systematically reviewed each stage of the monitoring pipeline. I first confirmed that AWS CloudTrail recorded the GetSecretValue event in Event History. Next, I verified that CloudTrail was successfully delivering logs to Amazon CloudWatch. I then checked whether the metric filter correctly detected the event and incremented the SecretIsAccessed metric. After that, I confirmed the CloudWatch alarm transitioned to the “In Alarm” state and had the correct action configured. Finally, I ensured that my Amazon Simple Notification Service subscription was confirmed and capable of delivering email notifications.

I initially didn’t receive an email before because my Amazon CloudWatch alarm statistic was set to Average instead of Sum. Using Average meant CloudWatch calculated the average rate of secret access over the evaluation period, which likely never crossed the threshold of ≥1, so the alarm never transitioned to the “In Alarm” state.

The key solution was changing the statistic to Sum, which adds up all occurrences of the SecretIsAccessed metric within the selected period. This ensures that even a single GetSecretValue event recorded from AWS Secrets Manager is enough to push the metric to 1 and trigger the alarm. Reducing the period from 5 minutes to 1 minute also made the alert more responsive, allowing the notification to be sent faster once the secret is accessed.

---

## Success!

To validate that my monitoring system works, I retrieved the secret again from AWS Secrets Manager to intentionally generate a GetSecretValue event.

I checked Amazon CloudWatch to confirm that the SecretIsAccessed metric increased and that the alarm changed to the “In Alarm” state.

I received an email notification through Amazon Simple Notification Service confirming that the alarm had been triggered, which verified that the full monitoring and notification pipeline was functioning correctly end to end.

![Image](http://learn.nextwork.org/sparkling_blue_joyful_nopal/uploads/aws-security-monitoring_ageraergearge)

---

## Comparing CloudWatch with CloudTrail Notifications

Amazon Simple Notification Service (SNS) notification delivery in AWS CloudTrail sends a message to your SNS topic every time a new log file is delivered to your S3 bucket. This simply confirms that CloudTrail has generated and stored a new log file — it does not analyse the contents of that file.

This is different from a CloudWatch alarm in Amazon CloudWatch, which triggers only when a specific pattern (such as GetSecretValue) is detected inside the logs.

In a project extension, I would enable SNS notification delivery for CloudTrail because it would give me confirmation that logging is functioning properly and that new audit logs are continuously being delivered, strengthening my overall monitoring and auditing setup.

After enabling CloudTrail SNS notifications, my inbox began receiving automated messages each time AWS CloudTrail delivered a new log file to my S3 bucket through Amazon Simple Notification Service.

In terms of the usefulness of these emails, I thought they were helpful for confirming that logging is active and functioning correctly, but they are not ideal for detecting specific security events. Unlike alarms from Amazon CloudWatch, these notifications do not indicate what action occurred — only that a log file was delivered.

![Image](http://learn.nextwork.org/sparkling_blue_joyful_nopal/uploads/aws-security-monitoring_d7e8f9g0)

---

---
