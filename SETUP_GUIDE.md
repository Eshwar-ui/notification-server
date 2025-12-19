# Step-by-Step Setup Guide

## 🔴 Current Error:
```
Error: Cannot find module './serviceAccountKey.json'
```

## ✅ Solution:

### Method 1: Download Service Account Key (Easiest)

1. **Open Firebase Console:**
   - Go to: https://console.firebase.google.com
   - Select your chat app project

2. **Navigate to Service Accounts:**
   - Click the **⚙️ gear icon** (top left)
   - Select **"Project Settings"**
   - Click the **"Service Accounts"** tab

3. **Generate Private Key:**
   - Click **"Generate New Private Key"** button
   - A warning dialog will appear - click **"Generate Key"**
   - A JSON file will download automatically

4. **Save the File:**
   - Rename the downloaded file to: `serviceAccountKey.json`
   - Move it to: `notification-server/serviceAccountKey.json`
   - The file should be in the same folder as `server.js`

5. **Verify the file exists:**
   ```bash
   cd notification-server
   dir serviceAccountKey.json  # Windows
   # or
   ls serviceAccountKey.json  # Linux/Mac
   ```

6. **Run the server again:**
   ```bash
   npm start
   ```

### Method 2: Using Environment Variable

If you prefer not to use a file:

1. **Copy the JSON content:**
   - Open the downloaded JSON file
   - Copy ALL the content

2. **Set environment variable (Windows PowerShell):**
   ```powershell
   $env:FIREBASE_SERVICE_ACCOUNT = @'
   {
     "type": "service_account",
     "project_id": "your-project-id",
     ...
   }
   '@
   ```

3. **Run server:**
   ```bash
   npm start
   ```

## 🎯 Expected Output:

After setup, you should see:
```
✅ Loaded service account from file
✅ Firebase Admin SDK initialized successfully
Notification server running on port 3000
```

## ⚠️ Security Notes:

- **NEVER** commit `serviceAccountKey.json` to Git (it's already in `.gitignore`)
- **NEVER** share your service account key publicly
- For production, use environment variables instead of files
- The service account key has admin access to your Firebase project

## 🐛 Troubleshooting:

**Error: "Cannot find module"**
- Make sure the file is named exactly `serviceAccountKey.json`
- Make sure it's in the `notification-server` folder
- Check the file path is correct

**Error: "Invalid credentials"**
- Make sure you downloaded the key from the correct Firebase project
- Regenerate the key if needed

**Error: "Permission denied"**
- Make sure the service account has "Firebase Cloud Messaging API Admin" enabled
- Check Firebase Console > APIs & Services > Enabled APIs

