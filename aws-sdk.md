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

Here's how to put an item into a DynamoDB table: 

    import { PutCommand } from '@aws-sdk/lib-dynamodb';
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
    putItem('YourTableName', { id: '123', name: 'John Doe' });
    

