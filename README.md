
# Serverless EMI Calculator using AWS Lambda and API Gateway

## Overview

This repository contains a serverless EMI calculator built with AWS Lambda and API Gateway. The application is designed to calculate the Equated Monthly Installment (EMI) based on principal, interest rate, and time period. It uses Python for the Lambda function and integrates with API Gateway to expose the functionality via HTTP requests.

## Documentation

- [Installation and Usage](Serverless_EMI_Calculator_using_AWS_Lambda_and_API_Gateway.md)


## Prerequisites

- AWS Account
- Basic understanding of AWS Lambda and API Gateway
- Python 3.9 runtime environment

## Steps to Deploy

### Step 1: Create AWS Lambda Function

1. **Login** to the [AWS Management Console](https://aws.amazon.com/console/).
2. **Search** for **Lambda** in the service bar.
3. **Create** a new Lambda function:
   - **Function Name:** `lambda-emi-calc`
   - **Runtime:** Python 3.9
   - Click **Create Function**.

### Step 2: Add Python Code

1. **Clear** existing code in the Lambda function editor.
2. **Paste** the following Python code:

    ```python
    import json
    print('Loading function... Lambda EMI calculator using API Gateway')

    def lambda_handler(event, context):
        # 1. Parse out query string params
        principal = int(event['queryStringParameters']['p'])
        rate = float(event['queryStringParameters']['r'])
        time = int(event['queryStringParameters']['t'])
        emi = emi_calculator(principal, rate, time)
        # 2. Construct the body of the response object
        transactionResponse = {
            'p': principal,
            'r': rate,
            't': time,
            'emi': emi
        }

        # 3. Construct http response object
        responseObject = {
            'statusCode': 200,
            'headers': {
                'Content-Type': 'application/json'
            },
            'body': json.dumps(transactionResponse)
        }
        # 4. Return the response object
        return responseObject

    def emi_calculator(p, r, t):
        r = r / (12 * 100)  # one month interest
        t = t * 12  # one month period
        emi = (p * r * pow(1 + r, t)) / (pow(1 + r, t) - 1)
        return emi
    ```

3. **Deploy** the Lambda function.

### Step 3: Test the Lambda Function

1. Configure a **test event** with the following input:

    ```json
    {  
      "queryStringParameters": {  
        "p": 10000,  
        "r": 2.5,  
        "t": 5  
      } 
    }
    ```

2. **Run** the test to ensure there are no errors and the output is correct.

### Step 4: Set Up API Gateway

1. **Search** for **API Gateway** in the service bar.
2. **Create** a new API Gateway:
   - **API Name:** `EmiCalcApi`
   - **Description:** `EmiCalcApi`
   - **Endpoint Type:** Regional
   - Click **Create API**.

3. **Create a Resource**:
   - **Resource Name:** `emi`
   - Click **Create Resource**.

4. **Create a Method**:
   - **Method Type:** GET
   - **Integration Type:** Lambda Function
   - **Lambda Proxy Integration:** Enabled
   - Select the Lambda function `lambda-emi-calc`.
   - Click **Create Method**.

### Step 5: Deploy the API

1. Click **Deploy API**.
2. **Stage Name:** `dev`
   - **Deployment Description:** `dev`
   - Click **Deploy**.

3. Go to the **Stage** section and click **Edit**.
4. **Update** parameters as needed:
   - **Rate (r):** Set to `5.8`
   - **Time (t):** Set to `10`

5. **Copy** the **Invoke URL** from the stage details and append the following query string:

    ```
    /emi?p=10000&r=5.8&t=10
    ```

6. **Paste** the complete URL into your browser to get the EMI result.

## Output

The Lambda function will return a JSON response with the EMI calculation, including the principal, rate, time, and calculated EMI.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
