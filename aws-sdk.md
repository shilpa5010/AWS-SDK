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

   
4. DynamoDB Example: Putting an Item
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
5. Lambda Example: Invoking a Lambda Function

To invoke a Lambda function:

           import { InvokeCommand } from '@aws-sdk/client-lambda';
        
        const invokeLambda = async (functionName, payload) => {
            const params = {
                FunctionName: functionName,
                Payload: Buffer.from(JSON.stringify(payload)),
            };
        
            try {
                const data = await lambdaClient.send(new InvokeCommand(params));
                console.log('Lambda response:', JSON.parse(Buffer.from(data.Payload).toString()));
            } catch (err) {
                console.error('Error invoking lambda:', err);
            }
        };
        
        // Usage
        invokeLambda('YourLambdaFunctionName', { key1: 'value1' });

6. SNS Example: Publishing a Message

Here's how to publish a message to an SNS topic:        
        
        import { PublishCommand } from '@aws-sdk/client-sns';
        
        const publishMessage = async (topicArn, message) => {
            const params = {
                Message: message,
                TopicArn: topicArn,
            };
        
            try {
                const data = await snsClient.send(new PublishCommand(params));
                console.log(`Message sent to the topic ${topicArn}. MessageID: ${data.MessageId}`);
            } catch (err) {
                console.error('Error publishing message:', err);
            }
        };
        
        // Usage
        publishMessage('arn:aws:sns:your-region:your-account-id:your-topic', 'Hello, SNS!');
        
### Conclusion        
These examples demonstrate basic operations for S3, DynamoDB, Lambda, and SNS using AWS SDK for JavaScript version 3. Remember to replace placeholders with your actual AWS resource details. Let me know if you need more specific examples or additional services!

            
        
