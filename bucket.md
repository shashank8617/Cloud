##uploading a static web page to a instance
```bash
create index.html
aws configure
#provide the access key and secret key
aws s3api put-object-acl --bucket awscli143 --key index.html --acl public-read
```
