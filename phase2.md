# 🔐 Add Authentication & Enable Claude 3 Sonnet on AWS

## 📝 **Overview**
Now that the React web app is deployed, you’ll:
- Add user authentication using **AWS Amplify Auth**, backed by **Amazon Cognito**.
- Customize user sign-up verification emails.
- Enable access to **Claude 3 Sonnet**, a powerful foundation model from **Anthropic**, via **Amazon Bedrock**.

---

## 🎯 **Goals (What You Will Accomplish)**
- ✅ Configure email-based authentication using Amplify Auth.
- ✅ Customize the verification email.
- ✅ Enable access to Claude 3 Sonnet via Amazon Bedrock in `us-east-1`.

---

## ⏱️ **Time Required**  
**~10 minutes**

---

## 🧰 **Pre-requisites**
- AWS Account
- Amplify CLI setup
- App deployed (e.g., `ai-recipe-generator`)
- Admin access to AWS Management Console

---

## 🛠️ **Implementation Steps**

---

### ✅ 1. Configure Authentication with Custom Email

1. Open the file:  
   `ai-recipe-generator/amplify/auth/resource.ts`

2. Replace contents with:
```ts
import { defineAuth } from "@aws-amplify/backend";

export const auth = defineAuth({
  loginWith: {
    email: {
      verificationEmailStyle: "CODE",
      verificationEmailSubject: "Welcome to the AI-Powered Recipe Generator!",
      verificationEmailBody: (createCode) =>
        `Use this code to confirm your account: ${createCode()}`,
    },
  },
});
```

> 📧 This customizes the **verification email** to include a **code** and personalized message.

---

### ✅ 2. Push Auth Changes to Amplify

Run in terminal:
```bash
amplify push
```
This will deploy the updated auth configuration to AWS Cognito.

---

### ✅ 3. Enable Claude 3 Sonnet in Amazon Bedrock

1. Go to [Amazon Bedrock Console](https://console.aws.amazon.com/bedrock/)
2. Ensure you’re in the **N. Virginia (us-east-1)** region.

![](https://i.postimg.cc/02X7dcT1/03.png)

3. Under **Foundation models**, click **Claude**.
4. Find the **Claude 3 Sonnet** tab and click:
   - **Request model access** (or **Manage model access** if already enabled).

![](https://i.postimg.cc/VNnMw1dz/04.png)

5. Choose the model (`Claude 3 Sonnet`) → Click **Next** → **Submit** on the Review page.

![](https://i.postimg.cc/8cKf4znm/06.png)

> 🧠 Claude 3 Sonnet offers high-performance text generation for recipe ideas, conversations, and more.

---

## ✅ **Conclusion**
You’ve successfully:
- Set up authentication for your app using Amplify Auth.
- Customized the email verification process for a branded experience.
- Requested access to **Claude 3 Sonnet** in Amazon Bedrock to enable AI-powered features in your app.

