#uploading a static web page to a instance
create index.html
```bash
aws configure
#provide the access key and secret key
```
```bash
aws s3api put-object-acl --bucket awscli143 --key index.html --acl public-read
```
