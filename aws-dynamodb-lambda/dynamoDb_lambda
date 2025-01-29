import os
import boto3
import json

def lambda_handler(event, context):
    # Load secret name from environment variable
    secret_name = os.getenv("AWS_SECRET_NAME")
    region_name = os.getenv("AWS_REGION", "us-east-1")  # Default to us-east-1

    if not secret_name:
        raise ValueError("AWS_SECRET_NAME environment variable is not set")

    # Create a Secrets Manager client
    secretClient = boto3.client(service_name="secretsmanager", region_name=region_name)

    get_secret_value_response = secretClient.get_secret_value(SecretId=secret_name)
    secret = json.loads(get_secret_value_response["SecretString"])

    Table_name = "studentlist_table"
    
    print("DynamoDB Table creation started.")
    
    dynamodb = boto3.resource(
        "dynamodb",
        aws_access_key_id=secret.get("Access Key"),
        aws_secret_access_key=secret.get("Secret Access Key"),
        region_name=region_name,
    )
    
    student_table = dynamodb.create_table(
        TableName=Table_name,
        KeySchema=[
            {"KeyType": "HASH", "AttributeName": "StudId"}
        ],
        AttributeDefinitions=[
            {"AttributeName": "StudId", "AttributeType": "N"}
        ],
        ProvisionedThroughput={"ReadCapacityUnits": 2, "WriteCapacityUnits": 2},
    )
    
    # Wait until the Table gets created
    student_table.meta.client.get_waiter("table_exists").wait(TableName=Table_name)
    print("DynamoDB Table Creation Completed.")
    
    print("Insert Student data to table started.")
    # Insert data into DynamoDB table
    table = dynamodb.Table(Table_name)
    students = [
        {"StudId": 100, "FirstName": "kevin", "LastName": "ONDERI", "Dept": "IT", "Age": 28},
        {"StudId": 200, "FirstName": "Sam", "LastName": "MWANGI", "Dept": "HR", "Age": 22},
        {"StudId": 300, "FirstName": "abdi", "LastName": "HUSSEIN", "Dept": "FINAC", "Age": 25},
    ]

    for student in students:
        table.put_item(Item=student)
    
    print("Student data inserted to table successfully.")
