# Configure CloudWatch Logs to collect and analyze logs from an EC2 instance running a web server. Demonstrate how to search and filter logs, create metric filters, and set up alarms based on specific log events (e.g., errors or warnings).

## to setup cloud logs 

* to install logs 

```bash
sudo yum install awslogs
```
* edit file /etc/awslogs/awscli.conf & change the region
```bash
vi /etc/awslogs/awscli.conf
```

* verify the file /etc/awslogs/awslogs.conf 
```bash
vi /etc/awslogs/awslogs.conf
```
```bash
sudo service awslogsd start
```
```bash
sudo systemctl enable awslogsd
```

## to deploy web page


```bash
vi setup.sh
```
```bash
#!/bin/bash

# Update the package index
yum update -y

# Install Apache web server
yum install -y httpd

# Enable Apache to start on boot
systemctl enable httpd

# Start Apache web server
systemctl start httpd

# Create a simple HTML file to serve as the demo web page
echo "<!DOCTYPE html>
<html>
<head>
    <title>Demo Web Page</title>
</head>
<body>
    <h1>Welcome to your Demo Web Page!</h1>
    <p>This is a simple web page deployed using user data on an EC2 instance.</p>
</body>
</html>" > /var/www/html/index.html

# Ensure the proper permissions for the web directory
chown -R apache:apache /var/www/html
chmod -R 755 /var/www/html
```
* Make the Script Executable and Run It
```bash
chmod +x setup.sh
./setup.sh
```
* Verify Apache and the Web Page & Check if Apache is running
```bash
systemctl status httpd
```
* Ensure the HTML file is in the correct location

```bash
ls /var/www/html
```
* to restart
```bash
sudo systemctl restart httpd
```




# Using AWS Management Console or CLI, create a CloudWatch alarm that triggers when CPU utilization on an EC2 instance exceeds 70% for more than 5 minutes. Configure the alarm to send notifications via Amazon SNS.


* Create an SNS Topic and Subscription

* Open the Amazon SNS console
* In the left navigation pane, choose Topics
* Choose Create topic
* Select the topic type (Standard or FIFO), give it a name, and choose Create topic
* Select the newly created topic, and then choose Create subscription
* Choose the protocol select Email enter the endpoint as email address and choose Create subscription
* Confirm the subscription by clicking the confirmation link sent to your email

** Create the CloudWatch Alarm

* Open the CloudWatch console
* In the left navigation pane, choose Alarms, then choose All alarms
* Choose Create alarm
* Choose Select metric
* In the Browse tab, choose EC2, then Per-Instance Metrics
* Select the CPUUtilization metric for the specific EC2 instance
* Click Select metric
* Configure the alarm
* Set Period to 5 minutes
* Under Conditions, set the threshold type to Static
* Enter 70 in the Greater than field
* Under Additional configuration, set the number of data points to 1 out of 1 click Next
* Under Notification, choose In alarm
* Select Select an existing SNS topic and choose the topic you created earlier
* Click Next, review the alarm configuration, and choose Create alarm





# Create a CloudWatch dashboard that displays key metrics (e.g., CPU utilization, network traffic) from multiple AWS services (e.g., EC2, S3). Customize the dashboard layout and widgets to provide a comprehensive overview of application performance.

* Open CloudWatch Dashboard

* Open the CloudWatch console
* In the navigation pane, choose Dashboards
* Click Create dashboard
* Enter a name for your dashboard and click Create dashboard
* Add Widgets to the Dashboard

** CPU Utilization (EC2)

* Click Add widget
* Select Line
* Click Configure
* In the Metrics tab, choose EC2
* Select Per-Instance Metrics
* Select CPUUtilization for the desired instance
* Click Create widget
* Network Traffic 

* Click Add widget
* Select Line
* Click Configure
* In the Metrics tab, choose EC2
* Select Per-Instance Metrics
* Select NetworkIn and NetworkOut for the desired instance
* Click Create widget
* S3 Bucket Size

* Click Add widget
* Select Number
* Click Configure
* In the Metrics tab, choose S3
* Select BucketSizeBytes
* Choose Average and Sum for the bucket(s) you want to monitor
* Click Create widget
* S3 Number of Objects

* Click Add widget
* Select Number
* Click Configure
* In the Metrics tab, choose S3
* Select NumberOfObjects
* Choose Average and Sum for the bucket you want to monitor
* Click Create widget
* Customize the Layout

* Drag and resize the widgets to create a layout 
* Click Save dashboard to save your layout

