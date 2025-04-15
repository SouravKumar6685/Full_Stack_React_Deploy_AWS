# 🛠️ Add Lambda Function & Connect to Claude 3 Sonnet via Amazon Bedrock

---

## 📝 **Overview**
You will now add custom backend logic using a **serverless function** via **AWS Lambda** and integrate it with **Amazon Bedrock** to invoke the **Claude 3 Sonnet** model using an HTTP request.

---

## 🎯 **What You Will Accomplish**
- ✅ Add Amazon Bedrock as a **GraphQL HTTP data source**
- ✅ Create a custom **Lambda function** to process recipe requests
- ✅ Configure **secure model access permissions**

---

## ⏱️ **Time Required**
**~10 minutes**

---

## 🧰 **Pre-requisites**
- Text editor (VS Code, Atom, Sublime, etc.)
- Amplify project already initialized
- Permissions to use Amazon Bedrock in **us-east-1**

---

## 🛠️ **Implementation Steps**

---

### ✅ 1. Create Lambda Logic for Recipe Generation

1. Navigate to your backend data folder:
```bash
cd ai-recipe-generator/amplify/data
```

2. Create a new file named:
```
bedrock.js
```

3. Paste the following code:
```ts
export function request(ctx) {
  const { ingredients = [] } = ctx.args;

  const prompt = `Suggest a recipe idea using these ingredients: ${ingredients.join(", ")}.`;

  return {
    resourcePath: `/model/anthropic.claude-3-sonnet-20240229-v1:0/invoke`,
    method: "POST",
    params: {
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        anthropic_version: "bedrock-2023-05-31",
        max_tokens: 1000,
        messages: [
          {
            role: "user",
            content: [
              {
                type: "text",
                text: `\n\nHuman: ${prompt}\n\nAssistant:`,
              },
            ],
          },
        ],
      }),
    },
  };
}

export function response(ctx) {
  const parsedBody = JSON.parse(ctx.result.body);
  return {
    body: parsedBody.content[0].text,
  };
}
```

![](https://i.postimg.cc/zGW3b75j/01.png)

> 🍳 This function will handle input from the frontend and call Claude 3 Sonnet via Amazon Bedrock for recipe ideas.

---

### ✅ 2. Update `backend.ts` to Register the Data Source

1. Open `amplify/backend.ts`  
2. Replace or update with:
```ts
import { defineBackend } from "@aws-amplify/backend";
import { data } from "./data/resource";
import { PolicyStatement } from "aws-cdk-lib/aws-iam";
import { auth } from "./auth/resource";

const backend = defineBackend({
  auth,
  data,
});

const bedrockDataSource = backend.data.resources.graphqlApi.addHttpDataSource(
  "bedrockDS",
  "https://bedrock-runtime.us-east-1.amazonaws.com",
  {
    authorizationConfig: {
      signingRegion: "us-east-1",
      signingServiceName: "bedrock",
    },
  }
);

bedrockDataSource.grantPrincipal.addToPrincipalPolicy(
  new PolicyStatement({
    resources: [
      "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-sonnet-20240229-v1:0",
    ],
    actions: ["bedrock:InvokeModel"],
  })
);
```

> 🔐 This gives the Lambda function the correct permissions to invoke Claude 3 via **Bedrock's secured API**.

---

### 🚀 3. Deploy Backend Changes

Run this in your terminal:
```bash
npx ampx sandbox --profilr default
```

![](https://i.postimg.cc/8c6gKyZX/02.png)

---

## ✅ **Conclusion**
You have now:
- Defined a custom **Lambda function** with Amplify.
- Integrated **Amazon Bedrock** as an HTTP data source.
- Enabled secure, prompt-based recipe generation via **Claude 3 Sonnet**.

