# Notification Server Setup

## Quick Start:

### Step 1: Install Dependencies
```bash
npm install
```

### Step 2: Get Firebase Service Account Key

**Option A: Download JSON File (Recommended for local development)**

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your project
3. Click the **gear icon** ⚙️ → **Project Settings**
4. Go to **Service Accounts** tab
5. Click **"Generate New Private Key"**
6. Save the downloaded JSON file as `serviceAccountKey.json` in this directory
7. **⚠️ IMPORTANT:** This file is already in `.gitignore` - never commit it!

**Option B: Use Environment Variable (Recommended for production)**

Instead of a file, you can set the service account as an environment variable:

```bash
# Windows PowerShell:
$env:FIREBASE_SERVICE_ACCOUNT = Get-Content serviceAccountKey.json -Raw

# Linux/Mac:
export FIREBASE_SERVICE_ACCOUNT=$(cat serviceAccountKey.json)
```

Or create a `.env` file (requires `dotenv` package):
```
FIREBASE_SERVICE_ACCOUNT={"type":"service_account","project_id":"..."}
```

### Step 3: Run the Server

```bash
npm start
# or for development with auto-reload:
npm run dev
```

You should see:
```
✅ Loaded service account from file
✅ Firebase Admin SDK initialized successfully
Notification server running on port 3000
```

### Step 4: Test the Server

Open another terminal and test:
```bash
# Windows PowerShell:
curl -Method POST -Uri http://localhost:3000/send-notification -ContentType "application/json" -Body '{"token":"test_token","title":"Test","body":"Hello"}'

# Linux/Mac:
curl -X POST http://localhost:3000/send-notification \
  -H "Content-Type: application/json" \
  -d '{"token":"test_token","title":"Test","body":"Hello"}'
```

### Step 5: Update Flutter App

In `lib/services/notification_service.dart`, update:
```dart
static const String notificationServerUrl = 'http://localhost:3000';
// For production: 'https://your-server.com'
```

### Step 6: Deploy (Optional)

**Heroku:**
```bash
heroku create your-app-name
heroku config:set FIREBASE_SERVICE_ACCOUNT="$(cat serviceAccountKey.json)"
git push heroku main
```

**Railway:**
- Connect your GitHub repo
- Add `FIREBASE_SERVICE_ACCOUNT` environment variable with JSON content
- Deploy

**Render:**
- Create new Web Service
- Set `FIREBASE_SERVICE_ACCOUNT` environment variable
- Deploy

## API Endpoints:

- `POST /send-notification` - Send to single token
  ```json
  {
    "token": "fcm_token_here",
    "title": "Notification Title",
    "body": "Notification Body",
    "data": { "key": "value" } // optional
  }
  ```

- `POST /send-notifications` - Send to multiple tokens
  ```json
  {
    "tokens": ["token1", "token2"],
    "title": "Notification Title",
    "body": "Notification Body",
    "data": { "key": "value" } // optional
  }
  ```

