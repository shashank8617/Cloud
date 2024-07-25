## Create CloudFront distribution for a static website hosted in an EC2,Deploy the nginx application on the ec2 instance. And use this to create CloudFront distribution.


```bash
sudo yum update -y
sudo amazon-linux-extras install nginx1
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```
* Create a Simple HTML File
```bash
sudo mkdir -p /usr/share/nginx/html
echo "<html><body><h1>Hello from EC2</h1></body></html>" | sudo tee /usr/share/nginx/html/index.html
```

* Verify Nginx Installation

* Open the browser and paste the public IP of your EC2 instance and the web page should be visible


* Open the CloudFront Console:

* Go to the CloudFront console.
* Create a New Distribution:

* Choose Create Distribution.
* Choose Get Started under the Web section.
* Configure the Distribution:

* Origin Settings:

* Origin Domain Name: Enter the public DNS name of your EC2 instance (e.g., ec2-xx-xxx-xxx-xxx.compute-1.amazonaws.com).
* Origin Path: Leave blank.
* Name: (optional) You can give your origin a name.
* HTTP and HTTPS: Choose HTTP only if your instance does not support HTTPS.
* Origin Protocol Policy: Set to HTTP only.
* Default Cache Behavior Settings:

* Viewer Protocol Policy: Set to Redirect HTTP to HTTPS or HTTP and HTTPS based on your requirements.
* Allowed HTTP Methods: Set to GET, HEAD.
* Cache Based on Selected Request Headers: Set to None.
* Distribution Settings:

* Price Class: Choose the price class based on your needs.
* Alternate Domain Names (CNAMEs): (optional) Add if you have custom domain names.
* SSL Certificate: Choose Default CloudFront Certificate or provide your own.
* Create the Distribution:

* Click Create Distribution.
* It may take several minutes for the distribution to be deployed.

* Verify CloudFront Distribution:
* Open your browser and navigate to the CloudFront distribution domain name.
* You should see the "Hello from EC2" message.







