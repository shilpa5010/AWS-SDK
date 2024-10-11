AWS Lambda allows you to run code in response to events without provisioning servers. Here are a few examples of using AWS Lambda with JavaScript (Node.js).

### Example 1: Basic Hello World Function

This Lambda function responds with a simple "Hello World" message.

```javascript
exports.handler = async (event) => {
    return {
        statusCode: 200,
        body: JSON.stringify({ message: "Hello, World!" }),
    };
};
```

### Example 2: Handling API Gateway Requests

This example demonstrates how to handle HTTP requests via API Gateway.

```javascript
exports.handler = async (event) => {
    const name = event.queryStringParameters && event.queryStringParameters.name ? event.queryStringParameters.name : 'World';
    
    return {
        statusCode: 200,
        body: JSON.stringify({ message: `Hello, ${name}!` }),
    };
};
```

### Example 3: Reading from DynamoDB

This function reads an item from a DynamoDB table.

```javascript
const AWS = require('aws-sdk');
const dynamoDB = new AWS.DynamoDB.DocumentClient();

exports.handler = async (event) => {
    const params = {
        TableName: 'YourTableName',
        Key: {
            id: event.pathParameters.id,
        },
    };

    try {
        const data = await dynamoDB.get(params).promise();
        return {
            statusCode: 200,
            body: JSON.stringify(data.Item),
        };
    } catch (error) {
        return {
            statusCode: 500,
            body: JSON.stringify({ error: 'Could not retrieve item' }),
        };
    }
};
```

### Example 4: Writing to S3

This function uploads a file to an S3 bucket.

```javascript
const AWS = require('aws-sdk');
const s3 = new AWS.S3();

exports.handler = async (event) => {
    const bucketName = 'your-bucket-name';
    const key = `uploads/${Date.now()}.txt`;
    const body = 'Hello, S3!';

    const params = {
        Bucket: bucketName,
        Key: key,
        Body: body,
    };

    try {
        await s3.putObject(params).promise();
        return {
            statusCode: 200,
            body: JSON.stringify({ message: 'File uploaded successfully!', key }),
        };
    } catch (error) {
        return {
            statusCode: 500,
            body: JSON.stringify({ error: 'File upload failed' }),
        };
    }
};
```

### Example 5: Processing SNS Messages

This example shows how to process messages from an SNS topic.

```javascript
exports.handler = async (event) => {
    for (const record of event.Records) {
        const message = record.Sns.Message;
        console.log('Received SNS message:', message);
        
        // Process the message (e.g., save to a database, trigger another service, etc.)
    }

    return {
        statusCode: 200,
        body: JSON.stringify({ message: 'Messages processed successfully!' }),
    };
};
```

### Deployment

To deploy these Lambda functions, you can use the AWS Management Console, AWS CLI, or tools like Serverless Framework or AWS SAM. Make sure to set the appropriate IAM roles and permissions for your Lambda functions to access the services they need.

Feel free to modify these examples based on your specific use cases!
