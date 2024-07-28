
CloudTrail

Enable AWS CloudTrail and Deliver Logs to an S3 Bucket
Create an S3 Bucket for CloudTrail Logs
Open the S3 console at https://console.aws.amazon.com/s3/.
Choose "Create bucket."
Enter a bucket name (e.g., cloudtrail-logs-demo) and choose the appropriate region.
Choose "Create bucket."
Enable CloudTrail
Open the CloudTrail console at https://console.aws.amazon.com/cloudtrail/.
Choose "Trails" in the left navigation pane.
Choose "Create trail."
Enter a name for the trail (e.g., MyCloudTrail).
In the "Storage location" section, for "S3 bucket," choose "Create new S3 bucket" or select the bucket you created (e.g., cloudtrail-logs-demo).
Choose "Create trail."
Create a CloudWatch Alarm for "DeleteBucket" Events
Create an IAM Role for CloudWatch to Read CloudTrail Logs
Open the IAM console at https://console.aws.amazon.com/iam/.
Choose "Roles" and then "Create role."
Choose "CloudWatch" as the service that will use this role.
Choose "Next: Permissions."
Add permissions for S3 and CloudWatch Logs:
Choose "Attach policies directly."
Select AmazonS3ReadOnlyAccess and CloudWatchLogsFullAccess.
Choose "Next: Tags," and then "Next: Review."
Enter a role name (e.g., CloudWatch-Read-CloudTrail) and choose "Create role."
Create a CloudWatch Log Group
Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.
In the navigation pane, choose "Logs" and then "Log groups."
Choose "Create log group."
Enter a name for the log group (e.g., CloudTrail/DeleteBucket) and choose "Create."
Create a CloudTrail Log Stream
In the same "Logs" section of the CloudWatch console, choose the log group you created (e.g., CloudTrail/DeleteBucket).
Choose "Actions" and then "Create log stream."
Enter a name for the log stream (e.g., DeleteBucketStream) and choose "Create log stream."
Set Up CloudTrail to Deliver Logs to CloudWatch
Open the CloudTrail console at https://console.aws.amazon.com/cloudtrail/.
Choose the trail you created (e.g., MyCloudTrail).
Choose "Edit" and scroll to the "CloudWatch Logs" section.
Choose "Configure."
For "Log group," select the log group you created (e.g., CloudTrail/DeleteBucket).
For "IAM role," select the role you created (e.g., CloudWatch-Read-CloudTrail).
Choose "Update trail."
Create a Metric Filter
Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.
In the navigation pane, choose "Logs" and then "Log groups."
Select the log group you created (e.g., CloudTrail/DeleteBucket).
Choose "Create metric filter."
Enter a filter pattern for "DeleteBucket" events: { ($.eventName = DeleteBucket) }.
Choose "Next" and configure the metric:
For "Metric namespace," enter CloudTrailMetrics.
For "Metric name," enter DeleteBucketEvents.
For "Metric value," enter 1.
Choose "Create filter."
Create an Alarm Based on the Metric Filter
Open the CloudWatch console at https://console.aws.amazon.com/cloudwatch/.
In the navigation pane, choose "Alarms" and then "Create alarm."
Choose "Select metric."
Choose "CloudTrailMetrics" and then "DeleteBucketEvents."
Choose "Select metric."
Configure the alarm:
For "Statistic," choose "Sum."
For "Period," choose "5 minutes."
For "Threshold type," choose "Static."
For "Whenever DeleteBucketEvents is," enter 1.
For "Additional configuration," configure actions to send notifications (e.g., using SNS).
Choose "Next" and configure alarm name and description.
Choose "Next" and review the settings.
Choose "Create alarm."
