# 🛠️ **Connect React App to AWS Amplify for Recipe Generation**

---

## 🎯 **What You Will Accomplish**
- ✅ Install Amplify client libraries in the React app.
- ✅ Implement user authentication flow for sign up, sign in, and password reset using Amplify UI components.
- ✅ Use the Amplify data client to invoke the GraphQL API (`askBedrock`) and generate recipes based on a list of ingredients.

---

## 🏁 **Steps for Implementation**

---

### ✅ 1. **Install Amplify Libraries**
To begin, install the necessary libraries for AWS Amplify in your React project.

1. Open a terminal window, navigate to the root of your project folder (`ai-recipe-generator`), and run the following command:
```bash
npm install aws-amplify @aws-amplify/ui-react
```

---

### ✅ 2. **Center UI Components in `index.css`**

1. Open `ai-recipe-generator/src/index.css` and update it to center the app UI:
```css
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.87);
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
}

.card {
  padding: 2em;
}

.read-the-docs {
  color: #888;
}
```

---

### ✅ 3. **Style the Ingredients Form in `App.css`**

1. Open `ai-recipe-generator/src/App.css` and add the following styles to design the ingredients form:
```css
.app-container {
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.header-container {
  padding-bottom: 2.5rem;
  margin: auto;
  text-align: center;
  align-items: center;
  max-width: 48rem;
}

.main-header {
  font-size: 2.25rem;
  font-weight: bold;
  color: #1a202c;
}

.search-container {
  display: flex;
  flex-direction: column;
  gap: 10px;
  align-items: center;
}

.wide-input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.search-button {
  width: 100%;
  max-width: 300px;
  padding: 10px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.result-container {
  margin-top: 20px;
  transition: height 0.3s ease-out;
  overflow: hidden;
}

.loader-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
```

---

### ✅ 4. **Add User Authentication in `main.tsx`**

1. Open `ai-recipe-generator/src/main.tsx` and update it with the following code to integrate the Amplify **Authenticator** component:
```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { Authenticator } from "@aws-amplify/ui-react";

ReactDOM.createRoot(document.getElementById("root")!).render(
  <React.StrictMode>
    <Authenticator>
      <App />
    </Authenticator>
  </React.StrictMode>
);
```

> ⚡ This wraps your `App` component inside the **Authenticator** component, which manages the entire authentication flow (sign-up, sign-in, MFA, etc.).

---

### ✅ 5. **Configure Amplify in `App.tsx`**

1. Open `ai-recipe-generator/src/App.tsx` and update the code to configure Amplify and handle the recipe generation form:
```tsx
import { FormEvent, useState } from "react";
import { Loader, Placeholder } from "@aws-amplify/ui-react";
import { Amplify } from "aws-amplify";
import { Schema } from "../amplify/data/resource";
import { generateClient } from "aws-amplify/data";
import outputs from "../amplify_outputs.json";
import "@aws-amplify/ui-react/styles.css";

Amplify.configure(outputs);

const amplifyClient = generateClient<Schema>({
  authMode: "userPool",
});

function App() {
  const [result, setResult] = useState<string>("");
  const [loading, setLoading] = useState(false);

  const onSubmit = async (event: FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    setLoading(true);

    try {
      const formData = new FormData(event.currentTarget);
      
      const { data, errors } = await amplifyClient.queries.askBedrock({
        ingredients: [formData.get("ingredients")?.toString() || ""],
      });

      if (!errors) {
        setResult(data?.body || "No data returned");
      } else {
        console.log(errors);
      }

    } catch (e) {
      alert(`An error occurred: ${e}`);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="app-container">
      <div className="header-container">
        <h1 className="main-header">
          Meet Your Personal
          <br />
          <span className="highlight">Recipe AI</span>
        </h1>
        <p className="description">
          Simply type a few ingredients using the format ingredient1,
          ingredient2, etc., and Recipe AI will generate an all-new recipe on
          demand...
        </p>
      </div>
      <form onSubmit={onSubmit} className="form-container">
        <div className="search-container">
          <input
            type="text"
            className="wide-input"
            id="ingredients"
            name="ingredients"
            placeholder="Ingredient1, Ingredient2, Ingredient3,...etc"
          />
          <button type="submit" className="search-button">
            Generate
          </button>
        </div>
      </form>
      <div className="result-container">
        {loading ? (
          <div className="loader-container">
            <p>Loading...</p>
            <Loader size="large" />
            <Placeholder size="large" />
          </div>
        ) : (
          result && <p className="result">{result}</p>
        )}
      </div>
    </div>
  );
}

export default App;
```

> ⚡ This code configures **Amplify** with the `amplify_outputs.json` file, which was generated earlier. It allows you to send ingredients from the form to the `askBedrock` query and display the generated recipe.

---

### ✅ 6. **Launch the Application**

1. In a new terminal, navigate to your project’s root directory and run:
```bash
npm run dev
```

2. Open the app in your browser at `http://localhost:3000`.

---

### ✅ 7. **Authentication Flow**

1. On the website, go to the **Create Account** tab, create a new user by entering your email and password, and then click **Create Account**.
2. You will receive a verification code via email. Enter the code to complete the sign-in process.

---

### ✅ 8. **Push Code to GitHub**

1. After testing the app, push the code changes to GitHub:
```bash
git add .
git commit -m 'connect to bedrock'
git push origin main
```

---

### ✅ 9. **Deploy via AWS Amplify**

1. Go to the [AWS Amplify Console](https://console.aws.amazon.com/amplify/apps) and select your app.
2. Amplify automatically builds and deploys your app.
3. Visit the deployed URL provided by Amplify to see your app live.

---

## ✅ **Conclusion**
You have successfully connected your **React app** to the **AWS Amplify backend**, implemented **user authentication**, and created a form that generates recipes based on a list of ingredients submitted by users.

