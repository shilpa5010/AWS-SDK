### AWS with SDK javascript version 3examples
## Here are some examples using the AWS SDK for JavaScript version 3 (v3). This version utilizes a modular architecture, which allows you to import only the services you need.

1. Setting Up the AWS SDK v3

First, install the necessary packages via npm:

    npm install @aws-sdk/client-s3 @aws-sdk/client-dynamodb @aws-sdk/client-lambda @aws-sdk/client-sns
    npm install @aws-sdk/lib-dynamodb

3. Configuring AWS SDK v3
    You can set up the SDK as follows:
   
        import { S3Client } from '@aws-sdk/client-s3';
        import { DynamoDBClient } from '@aws-sdk/client-dynamodb';
        import { LambdaClient } from '@aws-sdk/client-lambda';
        import { SNSClient } from '@aws-sdk/client-sns';
        
        const s3Client = new S3Client({ region: 'YOUR_REGION' });
        const dynamoDBClient = new DynamoDBClient({ region: 'YOUR_REGION' });
        const lambdaClient = new LambdaClient({ region: 'YOUR_REGION' });
        const snsClient = new SNSClient({ region: 'YOUR_REGION' });

   Import is not working so i have changed in the code as below

   
5. DynamoDB Example: Putting an Item
Example to create Table in DynamoDB.

https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-1.html

Here's how to put an item into a DynamoDB table: 

        const { DynamoDBClient } = require("@aws-sdk/client-dynamodb");
        const { PutCommand } = require("@aws-sdk/lib-dynamodb");
        const dynamoDBClient = new DynamoDBClient({ region: 'eu-west-2' });
        // We can also create table through code exampel is in this page in SDK module - https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-1.html
        
        
        const putItem = async (tableName, item) => {
            const params = {
                TableName: tableName,
                Item: item,
            };
        
            try {
                await dynamoDBClient.send(new PutCommand(params));
                console.log('Item added:', item);
            } catch (err) {
                console.error('Unable to add item:', err);
            }
        };
        
        // Usage
        putItem('user', { uid: 123, name: 'John Doe' }); //Integers shouldnt be in ''
3. S3 Example: Uploading a File

Here's how to upload a file to an S3 bucket:

        const Lambda = new AWS.Lambda();
        
        const invokeLambda = (functionName, payload) => {
            const params = {
                FunctionName: functionName,
                Payload: JSON.stringify(payload),
            };
        
            Lambda.invoke(params, (err, data) => {
                if (err) {
                    return console.error('Error invoking lambda: ', err);
                }
                console.log('Lambda response:', JSON.parse(data.Payload));
            });
        };
        
        // Usage
        invokeLambda('YourLambdaFunctionName', { key1: 'value1' });

            
        
