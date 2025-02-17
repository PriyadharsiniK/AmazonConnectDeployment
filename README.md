# AmazonConnect
Deployment Guide
1. Install the CloudFormation Template

The CloudFormation template will create the following resources in your AWS account:

DynamoDB Tables-2

Hours of Operation

Queues-4

Routing Profiles-4

Steps to Deploy the CloudFormation Stack:

Open the AWS CloudFormation Console.

Click Create stack → With new resources (standard).

Upload the CloudFormation YAML file provided in this repository.

Click Next, configure stack details (leave default unless needed), and click Next again.

Review the settings, acknowledge IAM permissions, and click Create Stack.

Wait for the stack status to become CREATE_COMPLETE.

2. Import the Contact Flow JSON into Amazon Connect

Once the CloudFormation stack is deployed, you need to manually import the contact flow.

Steps to Import the Contact Flow JSON:

Open the Amazon Connect Console and go to your instance.

Navigate to Routing → Contact Flows.

Click Create Contact Flow and give it a name.

Click Import Flow and upload the provided JSON file.

Save and publish the flow.

3. Upload the Lambda Zip Files in Lambda Console

Open the AWS Lambda Console.

Click Create Function → Author from Scratch.

Give it a name, choose Node.js/Python runtime (depending on your Lambda code).

Under Code Source, click Upload from → .zip file.

Upload the provided Lambda zip file and deploy.

Ensure the IAM role has permissions for Amazon Connect and DynamoDB access.

4. Import the Lex Bot Zip File into Amazon Lex Console

Open the AWS Lex Console.

Click Create Bot → Import Bot.

Upload the provided Lex zip file.

Click Create and ensure intents and slots are configured correctly.

Once deployed, copy the Lex bot ARN and reference it in the contact flow.

5. Insert Two Rows into the DynamoDB Table

Run the following AWS CLI commands to insert sample data into your OrderDetails table:

For macOS/Linux:

aws dynamodb put-item --table-name OrderDetails --item '{"OrderNo": {"S": "1297"}, "CustomerName": {"S": "John Doe"}, "Status": {"S": "Processed"}}'

aws dynamodb put-item --table-name OrderDetails --item '{"OrderNo": {"S": "1101"}, "CustomerName": {"S": "Lara Cameron"}, "Status": {"S": "Shipped"}}'

aws dynamodb put-item --table-name LoyaltyMembers --item '{"MemberID": {"S": "115296801"}, "MobileNo": {"S": "+1XXXXXXXXXX"}, "Name": {"S": "Joseph Murphy"}}'
replace XXXXXXXXXX with the mobile number with customer mobile number, who has to be treated as Loyalty Member.
For Windows CMD:
aws dynamodb put-item --table-name OrderDetails1 --item "{ \"OrderNo\": { \"S\": \"1297\" }, \"CustomerName\": { \"S\": \"John Doe\" }, \"Status\": { \"S\": \"Processed\" } }"

aws dynamodb put-item --table-name OrderDetails1 --item "{ \"OrderNo\": { \"S\": \"1101\" }, \"CustomerName\": { \"S\": \"Lara Cameron\" }, \"Status\": { \"S\": \"Shipped\" } }"

aws dynamodb put-item --table-name LoyaltyMembers --item "{ \"MemberID\": { \"S\": \"115296801\" }, \"MobileNo\": { \"S\": \"+1XXXXXXXXXX\" }, \"Name\": { \"S\": \"Joseph Murphy\" } }"
replace XXXXXXXXXX with the mobile number with customer mobile number, who has to be treated as Loyalty Member.

6. Claim a Phone Number and Attach the IV Inbound Flow

Open the Amazon Connect Console.

Navigate to Routing → Phone Numbers.

Click Claim a Number and select a number available in your region.

Once claimed, edit the phone number settings.

Under Contact Flow / IVR, select IV Inbound Flow (imported earlier).

Save the settings.

7. Verify Lambda and Lex Integration in the Contact Flow

Make sure the Invoke Lambda Function block references the correct Lambda ARN.

Ensure the Get Customer Input block references the correct Lex bot ARN.

Save and publish the flow after making the updates.

Test the setup by calling the claimed phone number. 