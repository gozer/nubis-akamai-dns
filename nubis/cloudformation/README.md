﻿# Working with Cloudformation

## Set Up
Before you deploy with Cloudformation you need to set up your parameters.json file. There is an example copy called parameters.json-dist that you can copy and edit. It should look something like this:

```json
[
  {
    "ParameterKey": "ServiceName",
    "ParameterValue": "skel"
  }, 
  {
    "ParameterKey": "Environment",
    "ParameterValue": "sandbox"
  }, 
  {
    "ParameterKey": "SSHKeyName",
    "ParameterValue": "my_key"
  },
  {
    "ParameterKey": "TechnicalOwner",
    "ParameterValue": "my-email@domain.dom"
  },
  {
    "ParameterKey": "AmiId",
    "ParameterValue": "ami-abcdef123"
  }
]
``` 

### ServiceName
The ServiceName is the name of this service. For Mozilla deployments this should be the name of a real service as noted in [inventory](https://inventory.mozilla.org/en-US/core/service/)

### Environment
The environment is one of *sandbox*, *stage* or *prod*. For this (and all manual deployments) you will set this to *sandbox*.

### SSHKeyName
This is the name of an existing ssh key that you have either created or uploaded to AWS.

### TechnicalOwner
The technical owner should be a valid email or distribution list which is monitored by the team responsible for maintaining this service.

### AmiId
You will collect this as output from nubis-builder. Once the build is complete nubis-builder will display the ami id which you will need to manually copy into the parameters.json file. You will need to do this after every successful build.

## Commands to work with CloudFormation

### Create
To create a new stack:
```bash
aws --region us-east-1 cloudformation create-stack --template-body file://nubis/cloudformation/main.json --parameters file://nubis/cloudformation/parameters.json --stack-name nubis-akamai-dns --capabilities CAPABILITY_IAM
```

### Update
To update and existing stack:
```bash
aws --region us-east-1 cloudformation update-stack --template-body file://nubis/cloudformation/main.json --parameters file://nubis/cloudformation/parameters.json --stack-name nubis-akamai-dns --capabilities CAPABILITY_IAM
```

### Delete
To delete the stack:
```bash
aws --region us-east-1 cloudformation delete-stack --stack-name nubis-akamai-dns
```

## Nested Stacks
We are using Cloudformation nested stacks to deploy the necessary resources. You can find the nested stack templates in the [nubis-stacks](https://github.com/Nubisproject/nubis-stacks) repository.
