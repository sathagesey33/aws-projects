# **AWS Lambda DynamoDB Integration **

## **Overview**

This project demonstrates how to integrate AWS Lambda with DynamoDB using AWS Secrets Manager to securely retrieve AWS credentials and perform operations like table creation and data insertion. The Lambda function  creates  DynamoDB table and inserts student data into the table.

## **Features**

- **DynamoDB Table Creation**:  creates the table.
- **AWS Secrets Manager Integration**: Retrieves AWS credentials from Secrets Manager securely.
- **Student Data Insertion**: Inserts sample student data into DynamoDB after ensuring the table exists.

## **Setup**

### **Pre-requisites**

- **AWS Account**: You need an AWS account and necessary IAM permissions.
- **AWS CLI**: Make sure you have the AWS CLI installed and configured with the appropriate credentials.
- **AWS Secrets Manager**: Store your AWS access key and secret access key in AWS Secrets Manager.
- **Python**: This Lambda function is written in Python, so ensure you have Python 3.x installed for local testing (optional).

### **Environment Variables**

Before deploying the Lambda function, make sure to set the following environment variables:

1. **`AWS_SECRET_NAME`**: The name of your secret in AWS Secrets Manager that contains your AWS credentials (Access Key and Secret Access Key).
2. **`AWS_REGION`** (optional): The AWS region where your resources are located (default is `us-east-1`).

You can configure these environment variables in the Lambda console under the "Configuration" tab or by using the AWS CLI.

### **Installation**

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/aws-dynamodb-lambda.git
   cd aws-lambda-dynamodb

2. Install the required dependencies:
    pip install boto3
3. Deploy the Lambda function using AWS Management Console, AWS CLI, or any other CI/CD tool.

### **Usage**
1. Create or Verify Secret in AWS Secrets Manager:
Ensure that your AWS access credentials are stored securely in AWS Secrets Manager under the secret name provided in the AWS_SECRET_NAME environment variable.

2. Deploy the Lambda Function:
Once the function is deployed, the Lambda will automatically createDynamoDB table (studentlist_table)   and insert sample student data into the table.

3. Testing:
You can trigger the Lambda function by configuring a test event in the Lambda console. The function will create the table and insert data, if needed.