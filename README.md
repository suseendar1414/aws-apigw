#AWS Services Learning Project.

This project serves as a hands-on tutorial for learning various AWS services, such as API Gateway, Lambda, and SNS. By following this guide, you will create an API using API Gateway and integrate it with Lambda functions, mock integrations, and SNS.

#Table of Contents
Overview
Prerequisites
Setup Steps
Create SNS Topic and Subscription
Create a Lambda Function
Set Up API Gateway
Mock Integration
Lambda Integration
SNS Integration
Deploy and Test the API
Conclusion


#Overview
This project demonstrates how to create and configure an API using AWS API Gateway with various integrations:

#Mock Integration: Returns a predefined response.
Lambda Integration: Executes a Lambda function.
SNS Integration: Sends a message to an SNS topic.
Prerequisites
AWS Account
Basic understanding of AWS services
Email for SNS subscription
Setup Steps
Create SNS Topic and Subscription
Create SNS Topic:

#Navigate to the Amazon SNS Console.
Create a new topic (choose "Standard").
Set the access policy to basic, allowing only the specified AWS account (your account ID) to publish and subscribe.
Create SNS Subscription:

#Create a subscription for the topic.
Choose Email as the protocol.
Enter the email address where you want to receive notifications.
Confirm the subscription by clicking the link sent to your email.
Create a Lambda Function
Navigate to AWS Lambda Console:

#Create a new Lambda function.
Set the function name, choose the runtime (e.g., Python 3.8), and architecture (x86_64).
Lambda Function Code:

#Use the following code for the Lambda function:

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'headers': {},
        'body': event['requestContext']['identity']['sourceIP'],
        'isBase64Encoded': False
    }

#Set Up API Gateway
Navigate to API Gateway Console:
Create a new REST API (choose "REST API" and not "REST API Private").
Set the API name and choose "Regional" for endpoint type.
Mock Integration
Create Mock Resource:
Create a new resource named mock.

Create a GET method under the mock resource.

Select "Mock" as the integration type.

Set up a mapping template with the following response:

{
    "statusCode": 200,
    "message": "This response is mocking you"
}


#Lambda Integration
Create Lambda Resource:
Create a new resource named lambda.
Create a GET method under the lambda resource.
Select "Lambda Function" as the integration type and choose the Lambda function created earlier.
SNS Integration
Create IAM Role for SNS and Lambda:

#Create a role that allows API Gateway to invoke SNS and Lambda.
Attach the necessary policies for SNS publish and Lambda invoke.
Create SNS Resource:

#Create a new resource named sns.
Create a POST method under the sns resource.
Select "AWS Service" as the integration type and configure it to use the created IAM role.
Set the integration request to pass query string parameters to SNS.
Deploy and Test the API
Deploy API:

#Click on "Deploy API" and create a new deployment stage.
Note the Invoke URL provided after deployment.
Test the API:

#Use the Invoke URL to test different endpoints (/mock, /lambda, and /sns).
Ensure each endpoint returns the expected responses.
Conclusion
You have now created and deployed an API using AWS API Gateway with mock, Lambda, and SNS integrations. This project helps you understand the basics of setting up and integrating various AWS services to build a functional API.

Feel free to expand on this project by adding more complex logic, additional services, or security configurations. Happy learning!
