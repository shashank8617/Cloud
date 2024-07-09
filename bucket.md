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
# if deletion is not possible
```bash
aws s3api delete-object --bucket awscli143 --key index.html --version-id YrBjHf0rymPCT6IEoZ79z9OZY0HNye
aws s3api delete-object --bucket awscli143 --key index.html --version-id 4C0JU0lbfUsRooWaKCRRcC7KUZIMl6
aws s3api delete-object --bucket awscli143 --key index.html --version-id 3c8G122T_M50RFKfRUJgTW0ops6GEO

```
### Verify Deletion
```bash
aws s3api list-object-versions --bucket awscli143
```

### Empty the Bucket:
```bash
aws s3 rm s3://awscli143 --recursive
```
### Delete the Bucket
```bash
aws s3 rb s3://awscli143
```
