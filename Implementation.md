# SETUP GUIDELINES for the roject, mapped to their technical functionalities.

### Stage 1: Infrastructure & Secrets Management


1. **Architecture Diagram**

**Functionality**: Provides a high-level visual overview of the end-to-end monitoring pipeline.


![1](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image1.png?raw=true)


2. **Secret Type Selection**
 
**Functionality**: Shows the selection of "Other type of secret" in AWS Secrets Manager.


![2](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image2.png?raw=true)


3. **Secret Configuration Review**

**Functionality**: Displays the naming and description of the `TopSecretInfo` secret.


![3](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image3.png?raw=true)


4. **Secret Details Dashboard**

**Functionality**: Confirms successful secret creation and displays the unique ARN.


![4](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image4.png?raw=true)



### Stage 2: Audit Logging & CloudTrail

These images prove the account is actively recording sensitive actions.

5. **CloudTrail Trail Details**

**Functionality**: Highlights the configuration of `secrets-manager-trail` and its S3 bucket storage.


![4](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image5.png?raw=true)


6. **CLI Secret Retrieval**

**Functionality**: Demonstrates a manual secret access attempt via AWS CloudShell to generate a log entry.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image6.png?raw=true)


7. **CloudTrail Event History**

**Functionality**: Shows the `GetSecretValue` event being correctly audited in the CloudTrail UI.


![4](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image7.png?raw=true)


8. **CloudWatch Log Event Inspection**

**Functionality**: Displays the raw JSON log structure as it is delivered to CloudWatch Logs.


 ![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image8.png?raw=true)



### Stage 3: Detection Metrics & Alarms

These images detail the transformation of logs into actionable security metrics.

9. **Metric Namespace Setup**

**Functionality**: Creating the `SecurityMetrics` namespace for the `Secret is accessed` metric.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image9.png?raw=true)


10. **Metric Filter Confirmation**

**Functionality**: Reviewing the final properties of the `GetSecretValue` log filter.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image10.png?raw=true)


11. **Filter Creation Success Banner**

**Functionality**: Confirms the metric filter is active within the log group.


 ![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image11.png?raw=true)


12. **Metric Selection for Alarm**

**Functionality**: Selecting the specific metric to begin the Alarm creation workflow.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image12.png?raw=true)


13. **Alarm Threshold Logic**

**Functionality**: Setting the alarm condition to trigger when access is `Greater/Equal than 1`.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image13.png?raw=true)



### Stage 4: Notifications & SOC Integration

These images document the alerting pathway to the security team.

14. **SNS Topic Creation**

**Functionality**: Creating the `SecurityAlarms` SNS topic for SOC communications.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image14.png?raw=true)


15. **Pending Subscription State**

**Functionality**: Shows the alarm in `Insufficient Data` while waiting for email confirmation.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image15.png?raw=true)


16. **SNS Confirmation Email**
    
**Functionality**: Displays the raw verification email sent by AWS to the SOC inbox.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image16.png?raw=true)


17. **Alarm "OK" State**

**Functionality**: Confirms the alarm is active and monitoring normally after verification.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image17.png?raw=true)


18. **Subscription Success Page**

**Functionality**: AWS confirmation page proving the email endpoint is officially subscribed.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image18.png?raw=true)



### Stage 5: Incident Response & Success Validation

These images prove the end-to-end functionality of the SIEM tool.

19. **Final Audit Validation**

**Functionality**: CloudTrail history showing multiple successful captures of secret access.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image19.png?raw=true)


20. **Security Incident Alert (ALARM)**

**Functionality**: The critical final alert email notifying the team of unauthorized access.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image20.png?raw=true)


21. **Email Inbox Overview**

**Functionality**: Displays the volume and timing of security alerts received in the inbox.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image21.png?raw=true)


22. **CloudTrail Notification Detail**

**Functionality**: Detailed view of an SNS notification containing CloudTrail log metadata.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image22.png?raw=true)


23. **S3 Log Storage Review**

**Functionality**: Navigating the S3 bucket where CloudTrail securely archives audit logs.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image23.png?raw=true)


24. **CloudWatch Alarm Metrics Graph**

**Functionality**: A visual graph showing the metric spike triggering the "In Alarm" state.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image24.png?raw=true)


25. **Final Notification JSON**

**Functionality**: Displays the structured JSON data sent in the final alert for SOC parsing.


![](https://github.com/D-rank-developer/AWS_SIEM_TOOL/blob/242538deea31592c3c8ce76902031f9d1bdf31a4/secrets/image25.png?raw=true)



