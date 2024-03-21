## Serverless Application Deployment Using AWS Lambda and API Gateway

This repository contains code for a serverless application deployed using AWS Lambda and AWS API Gateway. The application's backend is built using Node.js and utilizes AWS DynamoDB for data storage.

### Deployment Steps

1. **Packaging Code in AWS S3**

   The code is packaged and stored in an AWS S3 bucket to facilitate deployment. This ensures that the Lambda functions have access to the latest version of the codebase.

2. **Managing DynamoDB Tables**

   AWS DynamoDB is used as the database for this application. The necessary tables are created and managed within DynamoDB to store and retrieve data as required by the application.

3. **AWS CloudFormation Stack**

   AWS CloudFormation is used to manage the infrastructure as code. A CloudFormation stack is created to integrate the AWS Lambda functions and AWS API Gateway, ensuring seamless communication between the frontend and backend components of the application.

4. **Deploying Node.js API with AWS Lambda and API Gateway**

   The Node.js API is deployed as serverless AWS Lambda functions, which are triggered by API Gateway events. This architecture allows for scalable and cost-effective execution of the backend logic.

5. **Testing API Endpoints**

   Production-level testing of API endpoints is conducted using Postman. This involves sending various HTTP requests to the API endpoints to verify their functionality and ensure they meet the requirements of the application.

### Repository Structure

- **`/src`**: Contains the source code for the Node.js API functions.
- **`/cloudformation`**: Includes CloudFormation templates for infrastructure provisioning.
- **`/tests`**: Contains Postman collections for testing API endpoints.
- **`/docs`**: Documentation and README files.

### Getting Started

To deploy and test the serverless application locally, follow these steps:

1. Clone this repository to your local machine.
2. Install the necessary dependencies for the Node.js API functions.
3. Configure AWS credentials and set up the required AWS services (S3, DynamoDB, CloudFormation, Lambda, API Gateway).
4. Deploy the CloudFormation stack using the provided templates.
5. Use Postman to test the API endpoints and verify the application's functionality.

### Contributing

Contributions to this project are welcome! If you encounter any issues or have suggestions for improvements, please open an issue or submit a pull request.
