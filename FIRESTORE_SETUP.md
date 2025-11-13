# Firestore Setup Guide for Pageant Scoring App

This guide will help you set up Google Cloud Firestore for real-time data synchronization across multiple devices.

## Why Firestore?

✅ **Real-time sync** - All judges see updates instantly  
✅ **No server needed** - Google hosts everything  
✅ **Offline support** - Works offline, syncs when back online  
✅ **Free tier** - Generous limits, perfect for pageant events  
✅ **Multi-device** - Admins and judges on different devices share same data

---

## Step 1: Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Add project"** or **"Create a project"**
3. Enter a project name (e.g., `pageant-scoring-2025`)
4. Click **Continue**
5. Disable Google Analytics (optional) or leave it enabled
6. Click **Create project**
7. Wait for project creation, then click **Continue**

---

## Step 2: Enable Firestore Database

1. In your Firebase project, click **"Firestore Database"** from the left menu
2. Click **"Create database"**
3. Select **"Start in production mode"** (we'll update security rules next)
4. Choose a location (select closest to your event venue):
   - `us-central` for USA central
   - `us-east1` for USA east coast
   - `us-west1` for USA west coast
   - `asia-south1` for India
5. Click **"Enable"**

---

## Step 3: Update Firestore Security Rules

**Important:** This allows anyone with your event code to read/write. Perfect for your use case.

1. In Firestore Database, click the **"Rules"** tab
2. Replace the existing rules with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow anyone to read/write events (event code acts as password)
    match /events/{eventCode} {
      allow read, write: if true;
      
      // Allow anyone to write to audit log
      match /audit/{document} {
        allow read, write: if true;
      }
    }
  }
}
```

3. Click **"Publish"**

> **Note:** For production use with sensitive data, you should add Firebase Authentication and restrict based on user IDs. This simple setup is fine for controlled pageant events.

---

## Step 4: Get Your Firebase Configuration

1. Click the **⚙️ Settings icon** next to "Project Overview" (top left)
2. Select **"Project settings"**
3. Scroll down to **"Your apps"** section
4. Click the **Web icon** `</>` to add a web app
5. Enter an app nickname (e.g., `Pageant Scoring Web`)
6. **Do NOT** check "Firebase Hosting"
7. Click **"Register app"**
8. You'll see a `firebaseConfig` object that looks like:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSyA...",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123def456"
};
```

9. **Copy this entire object** (you'll paste it into the app)

---

## Step 5: Configure Your Pageant Scoring App

1. Open your Pageant Scoring App (the `index.html` file)
2. Sign in as **Admin** (default code: `ADMIN123`)
3. Click the **Settings** tab
4. In the **"Cloud Sync (Firestore)"** section:
   - Paste your Firebase config JSON into the textarea
   - Enter an **Event Code** (e.g., `pageant2025`, `gwf-seattle-2025`)
     - This code is like a password - share it with all judges/admins
     - Everyone using the same event code shares the same data
5. Click **"Enable Cloud"**
6. You should see: ✅ "Cloud sync enabled! Data synced successfully."

---

## Step 6: Connect Other Devices

### For Other Admins:
1. Open the app on their device
2. Sign in as Admin
3. Go to Settings → Cloud Sync
4. Paste the **same Firebase config**
5. Enter the **same Event Code**
6. Click "Enable Cloud"
7. Their data will sync with yours automatically!

### For Judges:
1. Open the app on their device
2. They can either:
   - Sign in as Judge (local only), then enable cloud in Settings
   - OR have an admin enable cloud first, then just sign in as Judge
3. All score entries sync in real-time!

---

## How It Works

```
┌─────────────┐         ┌──────────────┐         ┌─────────────┐
│  Admin #1   │────────>│   Firestore  │<────────│  Judge #1   │
│  (Laptop)   │         │   (Google)   │         │  (Phone)    │
└─────────────┘         └──────────────┘         └─────────────┘
                               ↑
                               │
                        ┌──────┴──────┐
                        │   Judge #2   │
                        │   (Tablet)   │
                        └──────────────┘
```

- All devices with same Event Code share data instantly
- Changes sync in ~500ms
- Works offline, syncs when reconnected
- All stored in Firestore under `events/{your-event-code}`

---

## Pricing & Limits

### Firebase Free Tier (Spark Plan):

| Resource | Free Tier Limit | Typical Pageant Use |
|----------|----------------|---------------------|
| **Storage** | 1 GB | ~1 MB (0.1% used) |
| **Reads** | 50,000/day | ~2,000 (4% used) |
| **Writes** | 20,000/day | ~500 (2.5% used) |
| **Deletes** | 20,000/day | ~10 (0.05% used) |

**You will stay FREE** for any normal pageant event! 🎉

Example calculation for 10 judges × 50 contestants × 5 rounds:
- Total scores: 2,500 score entries
- Reads (viewing results): ~5,000
- Writes (entering scores): ~2,500
- **Total cost: $0.00** ✅

---

## Troubleshooting

### "Failed to enable cloud"
- Check your Firebase config JSON is valid (proper quotes, no typos)
- Make sure Firestore is enabled in Firebase Console
- Verify security rules are published

### "Sync failed"
- Check internet connection
- Verify Firebase project is active
- Look at browser console (F12) for error messages

### Data not syncing between devices
- Confirm all devices use the **exact same Event Code** (case-sensitive!)
- Check that "Auto-sync" checkbox is enabled in Settings
- Click "Sync Now" button to force immediate sync

### Scores disappeared
- Data is in 3 places: localStorage, Firestore cloud, and other devices
- If you "Reset" local data, Firestore copy remains intact
- Re-enable cloud sync to restore from Firestore
- Always export JSON backups before major changes!

---

## Security Best Practices

For public/competitive events with sensitive data:

1. **Keep Event Code Secret** - Only share with authorized judges/admins
2. **Use a Strong Event Code** - e.g., `gwf-2025-secure-xk9p2m` instead of `pageant`
3. **Change Code After Event** - Disable old code, create new one for next event
4. **Export Backups** - Use "Export JSON" button regularly
5. **Firebase Authentication** (Advanced) - Consider adding email/password auth for high-stakes events

---

## Advanced: Firebase Authentication (Optional)

For extra security, you can enable Firebase Authentication:

1. In Firebase Console, enable **Authentication** → **Email/Password**
2. Update Firestore rules to require authentication
3. Modify app to use `firebase.auth().signInWithEmailAndPassword()`

This is overkill for most pageant events but available if needed.

---

## Support

- [Firebase Documentation](https://firebase.google.com/docs/firestore)
- [Firestore Pricing](https://firebase.google.com/pricing)
- [Firebase Console](https://console.firebase.google.com/)

---

## Quick Start Checklist

- [ ] Create Firebase project
- [ ] Enable Firestore Database
- [ ] Update security rules (copy from Step 3)
- [ ] Get Firebase config (the JSON object)
- [ ] Open app → Admin login → Settings tab
- [ ] Paste config + enter event code → "Enable Cloud"
- [ ] Share event code with judges/admins
- [ ] Test sync between two devices
- [ ] Start scoring! 🎭

---

**You're all set!** Your pageant scoring app now has real-time cloud sync across all devices. 🚀
