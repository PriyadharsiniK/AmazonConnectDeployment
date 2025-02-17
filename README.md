## 🏢 **Amazon Connect Contact Center Deployment Guide**

For Full Contact Center Documentation, Refer to [InterVision Contact Center Documentation](InterVision_Contact_Center.md)


### 🛠 **1. Install the CloudFormation Template**
The CloudFormation template will create the following resources in your AWS account:
- **2 DynamoDB Tables**
- **Hours of Operation**
- **4 Queues**
- **4 Routing Profiles**

#### **Steps to Deploy the CloudFormation Stack:**
1. Open the AWS **CloudFormation Console**.
2. Click **Create stack → With new resources (standard)**.
3. Upload the **CloudFormation YAML file** provided in this repository.
4. Click **Next**, configure stack details (leave default unless needed), and click **Next** again.
5. Review the settings, acknowledge IAM permissions, and click **Create Stack**.
6. Wait for the stack status to become `CREATE_COMPLETE`.

---

### 🔄 **2. Import the Contact Flow JSON into Amazon Connect**
Once the CloudFormation stack is deployed, you need to manually import the contact flow.

#### **Steps to Import the Contact Flow JSON:**
1. Open the **Amazon Connect Console** and go to your instance.
2. Navigate to **Routing → Contact Flows**.
3. Click **Create Contact Flow** and give it a name.
4. Click **Import Flow** and upload the provided JSON file.
5. Save and publish the flow.

---

### 🖥️ **3. Upload the Lambda Zip Files in Lambda Console**
1. Open the **AWS Lambda Console**.
2. Click **Create Function → Author from Scratch**.
3. Give it a **name**, choose **Node.js/Python** runtime (depending on your Lambda code).
4. Under **Code Source**, click **Upload from → .zip file**.
5. Upload the provided **Lambda zip file** and deploy.
6. Ensure the IAM role has permissions for **Amazon Connect and DynamoDB access**.
7. Copy the **Lambda ARN** and reference it correctly in the contact flow.

---

### 🤖 **4. Import the Lex Bot Zip File into Amazon Lex Console**
1. Open the **AWS Lex Console**.
2. Click **Create Bot → Import Bot**.
3. Upload the provided **Lex zip file**.
4. Click **Create** and ensure intents and slots are configured correctly.
5. Once deployed, copy the **Lex bot ARN** and reference it in the contact flow.

---

### 🗄️ **5. Insert Two Rows into the DynamoDB Table**

#### **For macOS/Linux:**

```sh
aws dynamodb put-item --table-name OrderDetails --item '{"OrderNo": {"S": "1297"}, "CustomerName": {"S": "John Doe"}, "Status": {"S": "Processed"}}' 

aws dynamodb put-item --table-name OrderDetails --item '{"OrderNo": {"S": "1298"}, "CustomerName": {"S": "Jane Smith"}, "Status": {"S": "Pending"}}'

aws dynamodb put-item --table-name LoyaltyMembers --item '{"MemberID": {"S": "115296801"}, "MobileNo": {"S": "+1XXXXXXXXXX"}, "Name": {"S": "Joseph Murphy"}}'
```
##### replace XXXXXXXXXX with the mobile number of the customer who has to be treated as Loyalty members. 

#### **For Windows CMD:**
```sh
aws dynamodb put-item --table-name OrderDetails1 --item "{ \"OrderNo\": { \"S\": \"1297\" }, \"CustomerName\": { \"S\": \"John Doe\" }, \"Status\": { \"S\": \"Processed\" } }"

aws dynamodb put-item --table-name OrderDetails1 --item "{ \"OrderNo\": { \"S\": \"1298\" }, \"CustomerName\": { \"S\": \"Jane Smith\" }, \"Status\": { \"S\": \"Pending\" } }"

aws dynamodb put-item --table-name LoyaltyMembers --item "{ \"MemberID\": { \"S\": \"115296801\" }, \"MobileNo\": { \"S\": \"+1XXXXXXXXXX\" }, \"Name\": { \"S\": \"Joseph Murphy\" } }"
```
##### replace XXXXXXXXXX with the mobile number of the customer who has to be treated as Loyalty members.
---

### 📞 **6. Claim a Phone Number and Attach the IV Inbound Flow**
1. Open the **Amazon Connect Console**.
2. Navigate to **Routing → Phone Numbers**.
3. Click **Claim a Number** and select a number available in your region.
4. Once claimed, **edit the phone number settings**.
5. Under **Contact Flow / IVR**, select **IV Inbound Flow** (imported earlier).
6. Save the settings.

---

### ✅ **7. Verify Lambda and Lex Integration in the Contact Flow**
- Make sure the **Invoke Lambda Function** block references the correct **Lambda ARN**.
- Ensure the **Get Customer Input** block references the correct **Lex bot ARN**.
- Save and publish the flow after making the updates.

---

**Test the setup by calling the claimed phone number.** 🚀

