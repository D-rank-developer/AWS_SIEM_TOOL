# 🔐 AWS Security Monitoring & Secret Access Detection System

------------------------------------------------------------------------

## 📌 Executive Summary

This project demonstrates the design and implementation of a real-time
cloud security monitoring solution to detect and alert on unauthorized
access to sensitive secrets within an AWS environment.

The solution showcases practical experience in:

-   Detection Engineering
-   Cloud Security Monitoring
-   Audit Logging & Compliance
-   Alert Automation
-   SOC-Oriented Incident Response

------------------------------------------------------------------------

# 🏗️ Security Architecture

### Core AWS Services Used

-   **AWS Secrets Manager** -- Secure secret storage
-   **AWS CloudTrail** -- API activity logging
-   **Amazon CloudWatch** -- Log monitoring & metric filtering
-   **Amazon SNS** -- Automated alert notification

------------------------------------------------------------------------
![Architecture](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image1.png?raw=true)

------------------------------------------------------------------------

# 🚀 Implementation Breakdown

## 🔹 1. Secure Secret Management

Created a secret (`TopSecretInfo`) using AWS Secrets Manager to
eliminate hard-coded credentials and align with secure configuration
best practices.

**Security Impact:** - Centralized sensitive credential storage
- Reduced risk of credential exposure
- Unique ARN tracking for auditability

------------------------------------------------------------------------

## 🔹 2. API Activity Logging & Audit Visibility

Configured CloudTrail (`secrets-manager-trail`) to log all management
events across the AWS account.

**Security Impact:** - Enabled full traceability of Secrets Manager
access
- Established audit-ready logging for forensic investigation

------------------------------------------------------------------------

## 🔹 3. Log Centralization

Integrated CloudTrail logs into a dedicated CloudWatch Log Group:

`nextwork-secretsmanager-loggroup`

This enabled near real-time log inspection and detection engineering.

------------------------------------------------------------------------

## 🔹 4. Detection Engineering

Created a CloudWatch Metric Filter to convert raw log events into
structured security metrics.

-   **Filter Pattern:** `"GetSecretValue"`
-   **Namespace:** `SecurityMetrics`
-   **Metric Name:** `SecretAccessCount`

This transformed audit logs into measurable security signals.

------------------------------------------------------------------------

## 🔹 5. Real-Time Alerting

Configured a CloudWatch Alarm with:

-   **Threshold:** ≥ 1 secret access within 1 minute
-   **Statistic:** Sum (ensures real-time detection)
-   **Evaluation Period:** 60 seconds

This guarantees immediate detection of sensitive API activity.

------------------------------------------------------------------------

## 🔹 6. Automated SOC Notification

Integrated Amazon SNS for automated escalation.

-   **SNS Topic:** `SecurityAlarms`
-   **Delivery Method:** Email-based SOC alerting
-   **Subscription Verification:** Confirmed to prevent abuse

Upon triggering, alerts were delivered within seconds.

------------------------------------------------------------------------

# ✅ End-to-End Validation

Performed controlled secret retrieval via AWS CLI:

``` bash
aws secretsmanager get-secret-value --secret-id TopSecretInfo
```

### Results:

-   CloudTrail logged the API call
-   CloudWatch metric incremented
-   Alarm transitioned to **ALARM** state
-   SNS delivered real-time security alert

This validated the full detection and escalation pipeline.

------------------------------------------------------------------------

# 📊 Security Capabilities Demonstrated

✔ Detection Engineering
✔ Cloud Security Monitoring
✔ Real-Time Alert Automation
✔ Audit & Compliance Readiness
✔ Incident Response Workflow Understanding

------------------------------------------------------------------------

# 🧠 Technical Skills Applied

-   AWS Security Architecture
-   CloudTrail Log Analysis
-   CloudWatch Metric Filters & Alarms
-   SNS Alert Automation
-   Security Event Detection Design
-   Cloud Compliance Monitoring

------------------------------------------------------------------------

# 🔎 Risk Context

Unauthorized secret access can lead to:

-   Credential compromise
-   Lateral movement
-   Privilege escalation
-   Data exfiltration

This implementation demonstrates practical ability to design
preventative detection controls aligned with SOC operations and
compliance standards.

------------------------------------------------------------------------

# 📈 Future Enhancements

-   Monitor IAM policy changes
-   Detect privilege escalation attempts
-   Integrate alerts into SIEM platforms
-   Implement automated response actions
-   Add anomaly detection for unusual secret access patterns

------------------------------------------------------------------------

# 🎯 Relevance to Cybersecurity Roles

This project reflects hands-on capability in:

-   Cloud Security Engineering
-   Security Operations (SOC)
-   Detection & Response
-   Monitoring Architecture
-   Audit & Governance Controls

It demonstrates the ability to move from risk identification to
technical detection implementation and operational alerting.
