# Using AWS Management Console or CLI, create a CloudWatch alarm that triggers when CPU utilization on an EC2 instance exceeds 70% for more than 5 minutes. Configure the alarm to send notifications via Amazon SNS.

```bash
sudo yum install awslogs
```
## edit file /etc/awslogs/awscli.conf & change the region
```bash
vi /etc/awslogs/awscli.conf
```

## verify the file /etc/awslogs/awslogs.conf 
```bash
vi /etc/awslogs/awslogs.conf
```
```bash
sudo service awslogsd start
```
```bash
sudo systemctl enable awslogsd
```

###Configure CloudWatch Logs to collect and analyze logs from an EC2 instance running a web server. Demonstrate how to search and filter logs, create metric filters, and set up alarms based on specific log events (e.g., errors or warnings).

```bash

```


###Create a CloudWatch dashboard that displays key metrics (e.g., CPU utilization, network traffic) from multiple AWS services (e.g., EC2, S3). Customize the dashboard layout and widgets to provide a comprehensive overview of application performance.

```bash

```
