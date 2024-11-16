# Serverless-AI-Model-Deployment-Using-Amazon-Bedrock-API-Gateway-AWS-Lambda-and-Postman-API
![AI model drawio](https://github.com/user-attachments/assets/abcedc56-c6b3-435d-abe9-29cd2ee3fd89)


This project demonstrates how to deploy a serverless AI model using Amazon Bedrock, API Gateway, AWS Lambda, and Postman to generate text-based responses from an AI model (Cohere model). This project showcases the use of AWS services to build a scalable and efficient solution for AI model deployment.

## Key Technologies & Services Used:
- **Amazon API Gateway**: Used to create the REST API to interact with the Lambda function.
- **AWS Lambda**: Serverless compute service used to run the AI model inference logic.
- **Amazon Bedrock**: Provides foundation models (e.g., Cohere model) to perform AI tasks such as generating responses.
- **IAM (Identity and Access Management)**: Manages permissions and roles for Lambda to interact with other AWS services.
- **Postman**: Tool to test the API and Lambda function by sending requests and receiving responses.

---

## Prerequisites
- AWS account with necessary permissions to create Lambda functions, IAM roles, and API Gateway.
- Postman for testing the API endpoints.
- Familiarity with AWS services, including Lambda, API Gateway, IAM, and Amazon Bedrock.

---

## Steps to Deploy

### Step 1: Request Access to AI Model in Amazon Bedrock
1. Go to **Amazon Bedrock** in your AWS account and navigate to **Base models** under **Foundation models**.
2. Request access to **Cohere** model, which will be used for generating text-based responses based on prompts.
3. Ensure that the model is available and ready to be used for this project.

### Step 2: Create IAM Role for Lambda Function
1. In the **IAM** console, go to **Roles** and create a new role with the name `ChatBot-Lambda-role-access`.
2. Select **Lambda** as the use case.
3. Add the following policies to the role:
   - **Bedrock permissions** (to interact with the Cohere model).
   - **CloudWatch Logs permissions** (for logging Lambda function execution).
4. Create the role and note down the role ARN.

### Step 3: Create Lambda Function
1. Go to **AWS Lambda** and create a new function using **Python** runtime.
2. Use the existing IAM role created in Step 2 (`ChatBot-Lambda-role-access`).
3. Set the timeout configuration to **1-2 minutes** and adjust the memory (e.g., **500 MB**).
4. Click **Create function**.

### Step 4: Create API Gateway
1. Go to **Amazon API Gateway** and select **Create API**.
2. Build a new **REST API** and create a resource with the path `/ask`.
3. Enable **CORS** (Cross-Origin Resource Sharing) for the resource.
4. Create a **POST method** and link it to the Lambda function.
5. Ensure **Lambda Proxy Integration** is enabled and select the correct region for Lambda.
6. Deploy the API by creating a new stage (e.g., **dev**).

### Step 5: Write and Deploy Lambda Code
1. Write the Lambda code in a Python file (e.g., `lambda_function.py`).
2. Refer to the file [lambda_function.py](./lambda_function.py) for the implementation.
3. Deploy the code to your Lambda function using the AWS Console or CLI.

### Step 6: Test the Lambda Function
1. Copy the **Invoke URL** from the API Gateway stage deployment.
2. Use **Postman** to send a **POST** request to the endpoint:
   - Append `/ask` to the Invoke URL.
   - Example payload:
     ```json
     {
       "Prompt": "History of London Tube Line?"
     }
     ```
3. Validate the response returned by the API.

---

## References
- [Cohere Model Parameters Documentation](https://docs.aws.amazon.com/bedrock/latest/userguide/model-parameters.html)
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Amazon API Gateway Documentation](https://docs.aws.amazon.com/apigateway/)
