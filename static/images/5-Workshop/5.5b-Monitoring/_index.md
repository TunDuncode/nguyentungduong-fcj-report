---
title : "Monitoring & Logging"
date : 2024-01-01
weight : 7
chapter : false
pre : " <b> 5.5b. </b> "
---

#### Goal

Set up monitoring so you can observe GameHub application health after deployment.

#### Detailed coverage

- Enable CloudWatch Logs for Lambda and API Gateway.
- Create metric filters for errors and latency.
- Configure alarms for incidents.
- Send notifications via SNS or email.

#### Implementation steps

1. Open CloudWatch Console.
2. Go to Logs > Log groups.
3. Select the Lambda or API Gateway log group.
4. Create a metric filter for failure patterns such as `ERROR` or HTTP `5xx`.
5. Create an alarm based on the metric filter.

#### Recommended alarms

- Lambda error rate > 1% over 5 minutes.
- API Gateway `5xx` rate > 5% over 5 minutes.
- CodePipeline deployment failures.

#### Notifications

- Use an SNS topic to send email or Slack alerts.
- Name alarms clearly, e.g. `GameHub-Lambda-Error-Alarm`.
- Review the CloudWatch dashboard regularly.

Note: Add a placeholder image for CloudWatch alarms in `images/5-Workshop/5.5b-Monitoring/cloudwatch-alarms.svg`.
