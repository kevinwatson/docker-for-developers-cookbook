### Chapter 7 - Cloud Development

## Introduction

### Storage

#### MinIO

MinIO is a service that provides file storage and has an Amazon Web Services (AWS) S3 compatible interface. You can run a Minio container locally, point your code at the local server and do all the testing you need before reconfiguring your code to consume a real AWS S3 bucket.

The following compose file starts a MinIO server and console which will print logging information to the terminal.

```
# docker-compose.yml
# usage: docker-compose up

version: "3.4"

services:
  minio:
    environment:
    - MINIO_ACCESS_KEY=ACCESS_KEY
    - MINIO_SECRET_KEY=SECRET_KEY
    - MINIO_HTTP_TRACE=/dev/stdout
    image: minio/minio:latest
    command: server /data
    ports:
    - 9000:9000
    stdin_open: true
    volumes:
    - minio-data:/data
  minio-console:
    image: minio/mc:latest
    entrypoint: /bin/sh -c "mc config host add minio http://minio1:9000 ACCESS_KEY SECRET_KEY && mc admin trace --all minio"
    stdin_open: true
    links:
    - minio:minio1
    depends_on:
    - minio
    volumes:
    - ./files:/var/files

volumes:
  minio-data:
```

Run the following lines of code in a new terminal to create a temporary S3 client using the official AWS S3 python package named `boto3`. As you interact with the MinIO server with the python code below, you can switch back to the other terminal to view the MinIO logging output.

```
docker run --rm -it --volume .:/home --net=host python:latest bash

pip install boto3 # install the s3 package

touch /home/test.tmp # create a temporary file that we'll upload to MinIO

python # run a python console

import boto3 # use the AWS S3 package
client = boto3.client('s3', aws_access_key_id='ACCESS_KEY', aws_secret_access_key='SECRET_KEY', endpoint_url='http://0.0.0.0:9000') # initialize a client with the keys defined in the docker-compose.yml file above and point it to our local MinIO server running on port 9000
bucket_name='my-bucket' # the bucket name we'll use
client.create_bucket(Bucket=bucket_name) # create the bucket
client.list_objects_v2(Bucket=bucket_name) # list objects in the bucket
client.put_object(Bucket=bucket_name, Key='test.tmp2', Body='/home/test.tmp') # upload a file
client.list_objects_v2(Bucket=bucket_name) # list objects in the bucket
```

## Resources

* https://min.io

[Next >>](080-chapter-08.md)
