# Deploy Notification Server

## 🚀 Quick Deploy Options

### Option 1: Railway (Recommended - Easiest)

**Free tier available, auto-deploys from GitHub**

1. **Sign up:** https://railway.app
2. **Create new project:**
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your `chatapp` repository
   - Select the `notification-server` folder

3. **Add environment variable:**
   - Go to your project → Variables
   - Add new variable:
     - **Name:** `FIREBASE_SERVICE_ACCOUNT`
     - **Value:** Copy the entire content of `serviceAccountKey.json` (the whole JSON object)

4. **Deploy:**
   - Railway will automatically detect it's a Node.js app
   - It will run `npm install` and `npm start`
   - Your server will be live at: `https://your-app-name.up.railway.app`

5. **Update Flutter app:**
   ```dart
   static const String notificationServerUrl = 'https://your-app-name.up.railway.app';
   ```

---

### Option 2: Render

**Free tier available**

1. **Sign up:** https://render.com
2. **Create new Web Service:**
   - Connect your GitHub repository
   - Select the `notification-server` folder
   - Build command: `npm install`
   - Start command: `npm start`

3. **Add environment variable:**
   - Go to Environment → Add Environment Variable
   - **Key:** `FIREBASE_SERVICE_ACCOUNT`
   - **Value:** Paste entire `serviceAccountKey.json` content

4. **Deploy:**
   - Render will build and deploy automatically
   - Your server will be at: `https://your-app-name.onrender.com`

5. **Update Flutter app:**
   ```dart
   static const String notificationServerUrl = 'https://your-app-name.onrender.com';
   ```

---

### Option 3: Heroku

**Requires credit card (but free tier available)**

1. **Install Heroku CLI:** https://devcenter.heroku.com/articles/heroku-cli

2. **Login:**
   ```bash
   heroku login
   ```

3. **Create app:**
   ```bash
   cd notification-server
   heroku create your-app-name
   ```

4. **Set environment variable:**
   ```bash
   # Copy your serviceAccountKey.json content
   heroku config:set FIREBASE_SERVICE_ACCOUNT="$(cat serviceAccountKey.json)"
   ```

5. **Deploy:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   heroku git:remote -a your-app-name
   git push heroku main
   ```

6. **Update Flutter app:**
   ```dart
   static const String notificationServerUrl = 'https://your-app-name.herokuapp.com';
   ```

---

### Option 4: Vercel

**Free tier, great for serverless**

1. **Install Vercel CLI:**
   ```bash
   npm i -g vercel
   ```

2. **Create `vercel.json` in notification-server folder:**
   ```json
   {
     "version": 2,
     "builds": [
       {
         "src": "server.js",
         "use": "@vercel/node"
       }
     ],
     "routes": [
       {
         "src": "/(.*)",
         "dest": "server.js"
       }
     ]
   }
   ```

3. **Deploy:**
   ```bash
   cd notification-server
   vercel
   ```

4. **Set environment variable:**
   - Go to Vercel dashboard → Your project → Settings → Environment Variables
   - Add `FIREBASE_SERVICE_ACCOUNT` with your JSON content

---

## 📋 Pre-Deployment Checklist

- [ ] Server code is ready (✅ already done)
- [ ] `package.json` has correct start script (✅ already done)
- [ ] Server uses `process.env.PORT` (✅ already done)
- [ ] Server supports environment variable for service account (✅ already done)
- [ ] `.gitignore` excludes `serviceAccountKey.json` (✅ already done)

---

## 🔐 Security Notes

### ✅ DO:
- ✅ Use environment variables for service account (not files)
- ✅ Never commit `serviceAccountKey.json` to Git
- ✅ Use HTTPS in production (most platforms provide this automatically)
- ✅ Keep your service account key secret

### ❌ DON'T:
- ❌ Commit service account key to repository
- ❌ Share your service account key publicly
- ❌ Use HTTP in production (use HTTPS)

---

## 🧪 Testing After Deployment

1. **Test the endpoint:**
   ```bash
   curl -X POST https://your-server.com/send-notification \
     -H "Content-Type: application/json" \
     -d '{
       "token": "test_token",
       "title": "Test",
       "body": "Hello"
     }'
   ```

2. **Update Flutter app:**
   - Change `notificationServerUrl` to your deployed URL
   - Restart the app
   - Send a message - notification should work!

---

## 🎯 Recommended: Railway

**Why Railway?**
- ✅ Free tier with generous limits
- ✅ Auto-deploys from GitHub
- ✅ Easy environment variable setup
- ✅ Automatic HTTPS
- ✅ No credit card required
- ✅ Simple dashboard

**Quick Start:**
1. Push your code to GitHub
2. Connect Railway to your repo
3. Select `notification-server` folder
4. Add `FIREBASE_SERVICE_ACCOUNT` environment variable
5. Deploy! 🚀

---

## 📱 After Deployment

Once deployed, update your Flutter app:

```dart
// lib/services/notification_service.dart
static const String notificationServerUrl = 'https://your-deployed-url.com';
```

Then:
- ✅ Works on any device
- ✅ Works from anywhere
- ✅ No localhost issues
- ✅ Production-ready!

