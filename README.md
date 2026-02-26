# CloudFormation Infrastructure as Code (IaC) - Template 

This project provides a CloudFormation template to deploy a serverless architecture on AWS. It includes an API Gateway, a Lambda function, and a DynamoDB table, along with the necessary IAM roles and permissions.

## Architecture

- **AWS API Gateway**: Exposes a RESTful endpoint (`POST`) that triggers the Lambda function.
- **AWS Lambda**: Processes incoming requests and interacts with the DynamoDB table.
- **AWS DynamoDB**: A NoSQL database table used for data storage.
- **IAM Roles & Policies**: Configured with specific permissions for DynamoDB, CloudWatch Logs, EC2, and S3 access.

## Prerequisites

- An AWS account.
- Lambda function code uploaded to an S3 bucket in `.zip` format.
- AWS CLI installed and configured (optional, for CLI deployment).

## Parameters

| Parameter | Description |
|-----------|-------------|
| `DynamoName` | The name of the DynamoDB table. |
| `DynamoKey` | The name of the partition key for the DynamoDB table. |
| `LambdaName` | The name of the Lambda function. |
| `LambdaRuntime` | The runtime environment for the Lambda (e.g., `python3.13`, `nodejs24.x`). |
| `LambdaBucket` | The S3 bucket name where the Lambda `.zip` file is stored. |
| `ZipName` | The name of the `.zip` file in the S3 bucket. |

## Deployment

### Using AWS Console
1. Log in to the AWS CloudFormation console.
2. Create a new stack and upload the `template.yml` file.
3. Fill in the required parameters.
4. Follow the prompts to create the resources.

### Using AWS CLI
```bash
aws cloudformation create-stack 
  --stack-name my-serverless-stack 
  --template-body file://template.yml 
  --parameters 
    ParameterKey=DynamoName,ParameterValue=MyTable 
    ParameterKey=DynamoKey,ParameterValue=id 
    ParameterKey=LambdaName,ParameterValue=MyFunction 
    ParameterKey=LambdaRuntime,ParameterValue=python3.13 
    ParameterKey=LambdaBucket,ParameterValue=my-code-bucket 
    ParameterKey=ZipName,ParameterValue=function.zip 
  --capabilities CAPABILITY_IAM
```

## Outputs
The stack exports several resources that can be used by other CloudFormation stacks:
- `LambdaPolicyDynamo`
- `LambdaPolicyEC2`
- `LambdaPolicyCW`
- `LambdaFunction` (ARN)
- `RootResourceId` (API Gateway ID)

## Author

**Kevin Sinza Salcedo** *Systems Engineer | Software Developer*

[LinkedIn](https://www.linkedin.com/in/kevin-sinza-967488105)