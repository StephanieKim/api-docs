## AWS Lambda
#### What is Lambda?

[AWS Lambda](https://aws.amazon.com/lambda) is a compute service that runs your code in response to events and automatically manages the compute resources for you, making it easy to build applications that respond quickly to new information.

### Algorithmia + Lambda
Algorithmia provides a built-in AWS Lambda Node.js blueprint, making it easy to call the Algorithmia API in response to events from Amazon Kinesis, Amazon DynamoDB, Amazon S3, and other Amazon web services.

For example, you could combine several algorithms from Algorithmia to:

* Automatically generate smart thumbnails (using face detection to ensure every thumbnail is perfectly cropped)
* Take advantage of Algorithmia’s speech-to-text algorithm to transcribe videos uploaded to S3 on the fly
* You could even leverage a predictive model every time DynamoDB updates.

Algorithmia and Lambda make it easy to rapidly build and deploy serverless solutions in minutes.

### Setup your Lambda function

#### Getting started

* Navigate to the [AWS Lambda console](https://console.aws.amazon.com/lambda/home)
* Select `Create a Lambda function`
* Type `Algorithmia` into the filter
* Select the Algorithmia blueprint
* Setup Auth in your Lambda function using the below guide
* Specify your algorithm and input data

### Authentication

#### Basic authentication

Set `apiKey` to your Algorithmia API key.
Also set `kmsEncryptedApiKey` to `null`.

> Basic authentication:

```
apiKey = "YOUR_API_KEY";
kmsEncryptedApiKey =  null;
```

#### Advanced authentication (more secure)

Follow these steps to encrypt your Algorithmia API Key for use in your function.

###### 1. Create a KMS key

Follow [this AWS guide](http://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html) to create your KMS key.

###### 2. Give your lAWS Lambda function execution role permission for the `kms:Decrypt` action

> Example Role:

```
{
    "Version": "2012-10-17",
    "Statement": [
    {
        "Sid": "Stmt1443036478000",
        "Effect": "Allow",
        "Action": [
            "kms:Decrypt"
        ],
        "Resource": [
            "<your KMS key ARN>"
        ]
    }
    ]
}
```

###### 3. Encrypt the event collector token using the AWS CLI

`aws kms encrypt --key-id alias/<KMS key name> --plaintext "<ALGORITHMIA_API_KEY>"`

###### 4. Copy the base-64 encoded, encrypted key (CiphertextBlob) to the `kmsEncryptedApiKey` variable

`kmsEncryptedApiKey = "<kmsEncryptedApiKey>";`

For more information, follow [this AWS Lambda walk through on our blog](http://blog.algorithmia.com/post/133832621114/get-started-building-intelligent-serverless-apps).