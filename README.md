# A SECURITY MONITORING TOOL TO SAFEGUARD SECRETS IN AWS
## Project Overview
In this project, I designed and implemented a centralized security monitoring solution using AWS native tools to address critical gaps in visibility. This system provides real-time threat detection and automated alerting, ensuring that sensitive data is protected and all administrative actions are audited.

Stage 1: Secret & Logging
Create a Secret
Secrets Manager is a secure AWS service that allowed me to safely store sensitive information. Instead of hard-coding credentials, I stored them here to maintain high security standards.

Selecting Secret Type: I chose "Other type of secret" to store custom configuration data.

Configuration: I named the secret TopSecretInfo and added a description for project tracking.

Confirmation: The secret was successfully created with a unique Amazon Resource Name (ARN).

Set Up CloudTrail
CloudTrail acts as the "black box" for my AWS account, recording every API call. I set up a trail named secrets-manager-trail to audit all access attempts to my sensitive data.

Stage 2: Verification & Monitoring
Testing Access via CloudShell
To verify the audit trail, I retrieved the secret value using the AWS CLI in CloudShell.

Analyzing the Audit Trail
In the CloudTrail Event History, I filtered by secretsmanager.amazonaws.com to locate the GetSecretValue event triggered by my previous command.

CloudWatch Log Integration
I verified that the logs were successfully flowing from CloudTrail to the centralized CloudWatch Log Group nextwork-secretsmanager-loggroup.

Stage 3: Detection & Alerting
Creating Metric Filters
I transformed raw log text into a numerical metric using a filter. I defined a filter pattern for "GetSecretValue" and assigned it to the SecurityMetrics namespace.

Defining the Metric:

Assigning Properties:

Creation Success:

Configuring the Alarm and SNS
I established a CloudWatch Alarm to trigger whenever the secret access metric recorded a value ≥ 1 within a 1-minute period.

Threshold Logic:

SNS Topic Creation: I created an SNS topic SecurityAlarms to forward these alerts to my SOC email.

Subscription Verification: To prevent spam, I verified the subscription via a confirmation email.

Final Validation & Success
Triggering the Alarm
I performed a final manual retrieval of the secret to test the end-to-end pipeline.

Receiving the Security Incident Alert
The system functioned perfectly: CloudTrail logged the event, CloudWatch detected the pattern, and SNS delivered an "ALARM" email to my inbox within seconds.

Operational Monitoring
I can now monitor these security events in real-time through the CloudWatch Alarm dashboard and confirm the state transitions.

Key Learning Outcomes
End-to-End Monitoring: I successfully designed a pipeline that detects, filters, and alerts on critical security events.

Incident Response: I learned that choosing the correct statistic (Sum vs. Average) is vital for real-time security alerting.

Compliance & Auditing: This implementation ensures my AWS account meets the "black box" standard for auditability and resource protection.
