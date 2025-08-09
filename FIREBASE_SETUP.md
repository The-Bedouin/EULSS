# Firebase Setup Guide for EULSS Resources Tool

## Overview
This guide will help you set up Firebase authentication and Firestore database so users can access their subjects and flashcards from any device.

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Enter a project name (e.g., "eulss-resources")
4. Choose whether to enable Google Analytics (optional)
5. Click "Create project"

## Step 2: Enable Authentication

1. In your Firebase project, click "Authentication" in the left sidebar
2. Click "Get started"
3. Click on "Email/Password" provider
4. Enable "Email/Password" authentication
5. Click "Save"

## Step 3: Create Firestore Database

1. Click "Firestore Database" in the left sidebar
2. Click "Create database"
3. Choose "Start in test mode" (for development)
4. Select a location close to your users
5. Click "Enable"

## Step 4: Get Your Firebase Config

1. Click the gear icon (⚙️) next to "Project Overview"
2. Select "Project settings"
3. Scroll down to "Your apps" section
4. Click the web icon (</>)
5. Register your app with a nickname (e.g., "EULSS Web App")
6. Copy the firebaseConfig object

## Step 5: Update Your Code

Replace the placeholder config in `resources.html` with your actual Firebase configuration:

```javascript
const firebaseConfig = {
  apiKey: "your-actual-api-key",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-actual-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "your-actual-sender-id",
  appId: "your-actual-app-id"
};
```

## Step 6: Set Up Security Rules (Optional but Recommended)

In Firestore Database > Rules, update the rules to:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## Features Enabled

✅ **User Registration & Login**: Users can create accounts and sign in
✅ **Cross-Device Access**: Data syncs to the cloud automatically
✅ **Data Persistence**: Subjects and flashcards are saved permanently
✅ **Real-time Sync**: Changes are immediately available on all devices
✅ **Secure Data**: Each user can only access their own data

## How It Works

1. **User creates account** → Firebase creates user profile
2. **User adds subjects/concepts** → Data saved to local storage + cloud
3. **User signs in on another device** → Data automatically loads from cloud
4. **Manual sync** → Users can force sync with the cloud
5. **Data persistence** → All data is safely stored and backed up

## Troubleshooting

### Common Issues:
- **"Firebase not initialized"**: Check if Firebase SDK scripts are loading
- **"Permission denied"**: Verify Firestore security rules
- **"Network error"**: Check internet connection and Firebase project status

### Testing:
1. Create an account on one device
2. Add some subjects and concepts
3. Sign out and sign in on another device
4. Verify your data appears

## Security Notes

- Users can only access their own data
- Passwords are securely hashed by Firebase
- All data is encrypted in transit
- Firebase handles authentication security

## Cost

- **Free tier**: 50,000 reads/day, 20,000 writes/day, 20,000 deletes/day
- **Paid tier**: $0.18 per 100,000 reads, $0.18 per 100,000 writes
- Most small to medium applications stay within free tier

## Support

- [Firebase Documentation](https://firebase.google.com/docs)
- [Firebase Console](https://console.firebase.google.com/)
- [Firebase Community](https://firebase.google.com/community)
