# **InterVision Ecommerce Contact Center Documentation**

## **Overview**
The **InterVision Ecommerce Contact Center** is designed to provide a seamless and intelligent customer support experience using **Amazon Connect, AWS Lambda, Amazon Lex, and DynamoDB**. The system ensures that **loyalty members** receive priority service, while other customers are assisted through a combination of automated and live agent interactions.

---

## **Call Flow Process**
### **1. Customer Calls the Contact Center**
- When a customer dials the **InterVision support number**, the call is received by **Amazon Connect**.
- A Lambda function is invoked immediately to check if the customer's **mobile number exists in the loyalty database (DynamoDB)**.

### **2. Loyalty Member Check (AWS Lambda)**
- If the caller **is a loyalty member**, they are routed to the **VIP Queue**, where skilled agents handle their inquiries with priority.
- If the caller **is not a loyalty member**, they are directed to an **Amazon Lex bot** to interact with self-service options.

### **3. Interactive Self-Service (Amazon Lex)**
The **Amazon Lex bot** presents the caller with multiple options:
- 📦 **Order Status Inquiry**
- 🔄 **Returns & Refunds**
- 💳 **Payment Issues**

### **4. Handling Customer Inquiries with Lex and Lambda**
#### **Order Status Inquiry**
- The **Lex bot prompts the customer** to enter their **Order Number**.
- A second **Lambda function is invoked**, which retrieves the **order status** from **DynamoDB** and provides a response to the customer.

#### **Returns & Payment Queries**
- Customers selecting **Returns** or **Payment Issues** are routed to specialized **queues** where skilled agents assist them.
- The system ensures that customers are directed to the right support team without unnecessary delays.

### **5. Callback Feature in the Queue**
- While waiting in the **queue**, customers are given the **option to request a callback**.
- If selected, the customer provides a **callback number**, which is stored as a **task** for agents.
- Agents are notified about pending callback requests and can return the call when available.

---

## **Technical Components Used**
### **Amazon Connect**
- Manages incoming customer calls and routes them based on customer type (loyalty vs non-loyalty).
- Provides call queuing and **callback options**.

### **AWS Lambda**
- First Lambda: **Checks the customer's mobile number** in DynamoDB to determine loyalty status.
- Second Lambda: **Fetches the order status** based on the order number provided by the customer.

### **Amazon DynamoDB**
- Stores **loyalty member data**.
- Stores **order details** for order status retrieval.

### **Amazon Lex**
- Provides **natural language understanding (NLU)** to enhance the self-service experience.
- Handles customer queries related to **order status, returns, and payment issues**.

---

## **Customer Experience Benefits**
✔ **VIP Treatment for Loyalty Members** → Faster support with skilled agents.  
✔ **Automated Self-Service Options** → Reduces agent workload and speeds up resolution.  
✔ **Intelligent Call Routing** → Ensures customers are directed to the right queue efficiently.  
✔ **Callback Feature** → Allows customers to request a return call instead of waiting on hold.  
✔ **AI-Powered Lex Bot** → Improves interaction with **natural language understanding (NLU)**.  

---

## **Conclusion**
The **InterVision Ecommerce Contact Center** is a customer-centric solution designed to provide **fast, intelligent, and efficient** customer service. By integrating **Amazon Connect, AWS Lambda, DynamoDB, and Lex**, this system ensures that customers receive the best possible support experience, whether through automated self-service or skilled human agents.

