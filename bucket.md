# uploading a static web page to a instance
create index.html and configure by providing access and secret key
```bash
aws configure
#provide the access key and secret key
```
```bash
aws s3api put-object-acl --bucket awscli143 --key index.html --acl public-read
```
```bash
aws s3 cp index.html s3://awscli143
```
```bash
https://awscli143.s3.ap-south-1.amazonaws.com/index.html
```
## to delete the file
```bash
aws s3 rm s3://awscli143/index.html
```
