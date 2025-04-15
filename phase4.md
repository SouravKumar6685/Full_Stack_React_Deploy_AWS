# 🛠️ **Configure GraphQL Query to Generate Recipes with Amazon Bedrock**

---

## 📝 **Overview**
In this task, you will define a **GraphQL query** to query the custom data source (Amazon Bedrock) and use it to generate recipes based on a list of ingredients. A custom type will be used to structure the response from Amazon Bedrock.

---

## 🎯 **What You Will Accomplish**
- ✅ Define a **GraphQL query** to take an array of ingredients.
- ✅ Create a **custom type** to structure the response from Bedrock.
- ✅ Connect the query with the custom handler defined earlier.

---

## ⏱️ **Time Required**
**~10 minutes**

---

## 🧰 **Pre-requisites**
- Amplify project with Lambda functions and Bedrock data source already configured.
- Familiarity with **GraphQL** and **AWS Amplify**.

---

## 🛠️ **Implementation Steps**

---

### ✅ 1. Define the GraphQL Query & Custom Type

1. Open your `ai-recipe-generator/amplify/data/resource.ts` file.

2. Update the file with the following code:
```ts
import { type ClientSchema, a, defineData } from "@aws-amplify/backend";

const schema = a.schema({
  // Define a custom type for Bedrock's response structure
  BedrockResponse: a.customType({
    body: a.string(),  // Contains the text response from Claude 3 Sonnet
    error: a.string(), // In case of an error, stores the error message
  }),

  // Define a query to ask Bedrock for a recipe based on ingredients
  askBedrock: a
    .query()
    .arguments({ ingredients: a.string().array() })  // Takes an array of ingredients
    .returns(a.ref("BedrockResponse"))  // Returns the BedrockResponse custom type
    .authorization((allow) => [allow.authenticated()])  // Requires authenticated access
    .handler(
      a.handler.custom({ entry: "./bedrock.js", dataSource: "bedrockDS" })  // Links to bedrock.js handler
    ),
});

export type Schema = ClientSchema<typeof schema>;

export const data = defineData({
  schema,
  authorizationModes: {
    defaultAuthorizationMode: "apiKey",  // Sets default API key authorization
    apiKeyAuthorizationMode: {
      expiresInDays: 30,  // API key expiration time
    },
  },
});
```

> ⚡ This code defines:
> - A **BedrockResponse** custom type to structure the response.
> - A **GraphQL query** `askBedrock` that takes an array of `ingredients` and returns the `BedrockResponse`.
> - Links to the **bedrock.js** Lambda handler that invokes Claude 3 Sonnet.

---

### ✅ 2. Deploy Cloud Resources with **npx ampx sandbox**

1. Open a new terminal window.

2. Navigate to your project's root directory:
```bash
cd ai-recipe-generator
```

3. Run the following command to deploy the cloud resources to a development sandbox:
```bash
npx ampx sandbox
```

> 🚀 This command will deploy the cloud resources into an isolated development space for rapid iteration.

4. Once the deployment is complete, your terminal will confirm the process, and the **amplify_outputs.json** file will be generated in your project directory.

---

## ✅ **Conclusion**
You have successfully configured a **GraphQL API** with a custom query to generate recipes using **Claude 3 Sonnet** via **Amazon Bedrock**. This setup allows you to:
- Send a list of ingredients via the `askBedrock` query.
- Receive a structured response with a generated recipe.
- Easily manage your cloud resources in an isolated development sandbox.
