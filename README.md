# ECR Upload To S3

[![Docker Automated buil](https://img.shields.io/docker/automated/atyagi/ecr-upload-to-s3.svg)](https://hub.docker.com/r/atyagi/ecr-upload-to-s3/)

Uploads ECR Docker credentials to S3. Inspired by [adobe-platform/aws-ecr-login](https://github.com/adobe-platform/aws-ecr-login)

Effectively creates a docker.tar.gz file from the authorization that is used when accessing private ECR repositories in [Marathon](https://mesosphere.github.io/marathon/) or [DC/OS](https://dcos.io).

## Environment Variables

Use these to change the behavior of the container.

### Required
- `REGISTRIES` - The 10 digit account id for the registry
- `S3_BUCKET` - The S3 bucket where the the file will live

### Optional
- `INTERVAL` - Change the interval, in seconds, for when the credentials will get updated. Defaults to 21600 (6 hours)
- `S3_PATH` - An optional path that sits underneath the S3 bucket 
- `AWS_ACCESS_KEY_ID` - If passed in, the aws cli commands will use this key
- `AWS_SECRET_ACCESS_KEY` - If passed in, the aws cli commands will use this secret key

## Examples for Running

```
docker run \
    -e "REGISTRIES=1234567890" \
    -e "S3_BUCKET=my-awesome-bucket" \
    atyagi/ecr-upload-to-s3
```

## Marathon JSON Example

```json
{
    "id": "ecr-upload-to-s3",
    "cpus": 0.1,
    "mem": 64,
    "instances": 1,
    "container": {
        "docker": {
            "network": "HOST",
            "image": "atyagi/ecr-upload-to-s3:latest"
        }
    },
    "env": {
        "REGISTRIES": "1234567890",
        "S3_BUCKET": "my-awesome-bucket"
    }
}
```
