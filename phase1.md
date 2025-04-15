# 🚀 Deploy a React App using AWS Amplify & GitHub

## 📝 **Overview**
AWS Amplify provides a **Git-based CI/CD** workflow to build, deploy, and host **single-page apps** (like React) or **static websites**.  
Once connected to a GitHub repository, Amplify:
- Auto-detects build settings.
- Builds frontend/backend.
- Deploys to a global CDN (`amplifyapp.com` domain).
- Updates on every `git push`.

---

## 🎯 **Goals (What You Will Accomplish)**
- ✅ Create a React application using Vite.
- ✅ Initialize and push code to GitHub.
- ✅ Connect GitHub repo to AWS Amplify.
- ✅ Deploy to a global CDN using Amplify hosting.

---

## ⏱️ **Time Required**  
**~5 minutes**

---

## 🧰 **Pre-requisites**
- GitHub account
- SSH access to GitHub
- Node.js & npm installed

---

## 🛠️ **Implementation Steps**

---

### ✅ 1. Create a Vite + React App (with TypeScript)
```bash
npm create vite@latest ai-recipe-generator -- --template react-ts -y
cd ai-recipe-generator
npm install
npm run dev
```
➡️ Open the **Localhost link** in the terminal to preview the app.

---

### ✅ 2. Push App to GitHub

1. Go to GitHub and create a **public repo**:  
   - Name: `ai-recipe-generator`  
   - Select: **Public**  
   - Click: **Create repository**

2. In your terminal:
```bash
git init
git add .
git commit -m "first commit"
git remote add origin git@github.com:<your-username>/ai-recipe-generator.git
git branch -M main
git push -u origin main
```

![](https://i.postimg.cc/FKMfC6Zw/01.png)

> 💡 Replace `<your-username>` with your GitHub username and use SSH URL.

---

### ✅ 3. Add Amplify to the App
```bash
npm create amplify@latest -y
```

![](https://i.postimg.cc/Pqshgngb/02-Npm-Amplify.png)

This will scaffold a lightweight Amplify project.

![](https://i.postimg.cc/jdDbCjKQ/03-FS.png)

Push the changes:
```bash
git add .
git commit -m "installing amplify"
git push origin main
```

![](https://i.postimg.cc/pryg90NX/04-Repo.png)

---

### ✅ 4. Connect GitHub Repo to AWS Amplify

1. Go to [AWS Amplify Console](https://console.aws.amazon.com/amplify/apps).

![](https://i.postimg.cc/DZwNDCwd/01.png)

2. Click **Create new app**.

![](https://i.postimg.cc/j2GkDtQZ/02.png)

3. Select **GitHub** as the source → Click **Next**.

![](https://i.postimg.cc/RZxD9C00/03.png)

4. Authenticate with GitHub → Choose your repo (`ai-recipe-generator`) and branch (`main`) → Click **Next**.

![](https://i.postimg.cc/Zq5ttYfd/04.png)


![](https://i.postimg.cc/wTXS1RZN/06.png)

5. Use default build settings → Click **Next**.
6. Review all info → Click **Save and deploy**.

🔄 Amplify will now:
- Build your app.
- Deploy it to: `https://<random-id>.amplifyapp.com`.
- Update on every `git push`.

---

### ✅ 5. Verify Deployment
- After build completes (may take ~5 mins), click **Visit deployed URL**.

![](https://i.postimg.cc/zvmcBqkp/07.png)

![](https://i.postimg.cc/BbGm3MqV/08.png)

- Your app is now live on the cloud 🌍.

![](https://i.postimg.cc/wTgwbf4t/09.png)

---

## ✅ **Conclusion**
You’ve successfully:
- Built a React app using Vite + TypeScript.
- Hosted it using AWS Amplify.
- Enabled auto-deployments with GitHub CI/CD.

With Amplify:
- Hosting is **global** and **automatic**.
- Every commit triggers a new deployment.
- Ideal for **modern frontend development** in the cloud.
