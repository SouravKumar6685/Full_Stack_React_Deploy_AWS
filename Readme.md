# 🚀 Deploy a React App using AWS Amplify & GitHub

### AI Recipe Generator using AWS Amplify and Amazon Bedrock

## Overview

In this tutorial, you will learn how to build a serverless web application using **AWS Amplify** and **Amazon Bedrock**, powered by the **Claude 3 Sonnet** foundation model. This application allows users to input a list of ingredients, and the system will generate delicious recipes based on the given ingredients. The application consists of:

- A **frontend** UI for ingredient submission.
- A **backend** to invoke the generative AI model (Claude 3 Sonnet) and generate recipes.


1[](https://d1.awsstatic.com/Getting%20Started/tutorials/build-a-basic-web-app-tutorial/build-basic-app-1.3078e53361b13f9fde6669cba0a570268ecc0d69.png)

### What you will accomplish

By following this tutorial, you will:

1. Configure **AWS Amplify** to host your frontend application with continuous deployment.
2. Set up **Amplify Auth** and enable access to the **Amazon Bedrock** foundation model.
3. Build a **serverless backend** for handling recipe generation requests.
4. Use **Amplify Data** to connect the frontend with the backend.
5. Deploy the application, enabling users to interact with the AI-powered recipe generator.

---

## Prerequisites

Before you begin, you will need:

- **An AWS account**: If you don't have one, [set up your environment](https://aws.amazon.com/getting-started/) by creating an AWS account.
- **AWS CLI configured**: Ensure your AWS profile is configured for local development.
- **Node.js and npm installed** on your machine.
- **Git** and a **GitHub account** (for version control and deploying the app).
- **Basic AWS experience** is helpful but not required.

### Time to complete
- **35 minutes**

### Cost to complete
- Free Tier eligible

### Requires
- **AWS account with administrator-level access**
- **AWS profile configured**
- **Node.js and npm**
- **GitHub account**

Note: If your AWS account is newly created (within the past 24 hours), some services might not be immediately available for use.

### Services used
- **AWS Amplify**
- **AWS Cognito**
- **AWS AppSync**
- **AWS Lambda**
- **Amazon Bedrock**

_Last updated: July 19, 2024_

---

## Application Architecture

The application architecture integrates several AWS services to create a seamless, serverless experience:

- **AWS Amplify**: Used for both frontend hosting and backend integration.
- **Amazon Bedrock**: Handles the AI-driven recipe generation using the Claude 3 Sonnet model.
- **AWS Lambda**: Executes the backend logic for processing ingredient lists.
- **AWS AppSync**: Provides the GraphQL API for interaction between the frontend and backend.
- **AWS Cognito**: Manages user authentication for accessing the application securely.

The following diagram visualizes the services involved:

![Architecture Diagram](architecture-diagram.png)

---

## Tasks Overview

This tutorial is divided into the following tasks. Each step builds upon the previous one to help you complete the entire workflow:

### 1. Host a Static Website (5 minutes)
- Configure **AWS Amplify** to host your frontend application with continuous deployment.

### 2. Manage Users (5 minutes)
- Set up **Amplify Auth** to handle user authentication and enable access to the **Amazon Bedrock** foundation model.

### 3. Build a Serverless Backend (10 minutes)
- Build an **AWS Lambda** function to handle ingredient submissions and invoke **Amazon Bedrock** to generate recipes.

### 4. Call the API from the Static Website (5 minutes)
- Use **Amplify Data** to interact with the backend API and trigger the recipe generation request.

### 5. Build the Frontend (5 minutes)
- Connect the frontend interface to the backend, allowing users to input ingredients and receive generated recipes.

### 6. Clean up Resources (2 minutes)
- Clean up the resources used in this tutorial to avoid any unwanted costs.

---

## Step-by-Step Instructions

### Task 1: Host a Static Website
- Configure **AWS Amplify** to automatically deploy your React application with continuous deployment linked to your GitHub repository.

### Task 2: Manage Users
- Set up  for user authentication and authorize users to interact with your application securely.

### Task 3: Build a Serverless Backend
- Set up invoke the **Claude 3 Sonnet** model through **Amazon Bedrock**.

### Task 4: Call the API from the Static Website
- Use **Amplify Data** to make API calls from your frontend, passing ingredient data to the serverless backend for processing.

### Task 5: Build the Frontend
- Create a form in the frontend where users can input a list of ingredients and display the AI-generated recipe on submission.

### Task 6: Clean up Resources
- Delete the resources used during this tutorial, including the **Amplify app** to prevent unwanted charges.

---

## Conclusion

By following the steps outlined in this tutorial, you have successfully built a **serverless web application** powered by **AWS Amplify** and **Amazon Bedrock**. This application allows users to generate recipes based on a list of ingredients through a seamless AI-powered process. You’ve learned how to configure frontend hosting, manage user authentication, integrate with backend APIs, and deploy the app using **AWS services**.

Feel free to explore further customizations and optimizations to enhance the user experience and functionality of your AI recipe generator!

---

## Next Steps

- **Explore further AI models**: Experiment with different **Amazon Bedrock** models to generate more personalized other types of content.
- **Deploy to production**: Set up a custom domain for your application and deploy it to production using **AWS Amplify**.

---

## Clean Up Resources

Don't forget to clean up your AWS resources to avoid any unnecessary charges. You can do this by deleting the **Amplify app** and associated services, such as **Lambda**, **Cognito**, **API Gateway**, and **DynamoDB** tables (if used).
