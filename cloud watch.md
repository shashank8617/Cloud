# Using AWS Management Console or CLI, create a CloudWatch alarm that triggers when CPU utilization on an EC2 instance exceeds 70% for more than 5 minutes. Configure the alarm to send notifications via Amazon SNS.


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




###Configure CloudWatch Logs to collect and analyze logs from an EC2 instance running a web server. Demonstrate how to search and filter logs, create metric filters, and set up alarms based on specific log events (e.g., errors or warnings).

```bash

```


###Create a CloudWatch dashboard that displays key metrics (e.g., CPU utilization, network traffic) from multiple AWS services (e.g., EC2, S3). Customize the dashboard layout and widgets to provide a comprehensive overview of application performance.

```bash

```
