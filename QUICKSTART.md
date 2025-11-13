# Quick Start Guide - Pageant Scoring with Firestore

Get your pageant scoring app running with cloud sync in under 10 minutes!

## 🎯 What You'll Get

✅ Real-time score sync across all devices  
✅ Multiple judges scoring simultaneously  
✅ Automatic backup to Google Cloud  
✅ Works offline, syncs when online  
✅ 100% FREE for typical pageant events

---

## 📋 Prerequisites

- [ ] Gmail account (for Firebase)
- [ ] Modern web browser (Chrome, Firefox, Safari, Edge)
- [ ] Internet connection (for initial setup)

---

## ⚡ 5-Minute Setup

### Step 1: Create Firebase Project (2 minutes)

1. Go to https://console.firebase.google.com/
2. Click **"Add project"**
3. Name it: `pageant-scoring-2025`
4. **Disable** Google Analytics (optional)
5. Click **"Create project"**

### Step 2: Enable Firestore (1 minute)

1. Click **"Firestore Database"** in left menu
2. Click **"Create database"**
3. Choose **"Production mode"**
4. Select your region (closest to event location)
5. Click **"Enable"**

### Step 3: Update Security Rules (1 minute)

1. Click **"Rules"** tab in Firestore
2. Paste this code:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /events/{eventCode} {
      allow read, write: if true;
      match /audit/{document} {
        allow read, write: if true;
      }
    }
  }
}
```

3. Click **"Publish"**

### Step 4: Get Firebase Config (1 minute)

1. Click ⚙️ icon → **"Project settings"**
2. Scroll to **"Your apps"**
3. Click Web icon `</>`
4. Name: `Pageant Scoring`
5. **Don't** check Firebase Hosting
6. Click **"Register app"**
7. **COPY** the `firebaseConfig` object (looks like this):

```javascript
{
  apiKey: "AIzaSyA...",
  authDomain: "pageant-scoring-2025.firebaseapp.com",
  projectId: "pageant-scoring-2025",
  storageBucket: "pageant-scoring-2025.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
}
```

### Step 5: Configure Your App (30 seconds)

1. Open `index.html` in browser
2. Login as Admin (code: `ADMIN123`)
3. Click **Settings** tab
4. Paste Firebase config in textarea
5. Enter event code: `myevent2025` (or any unique name)
6. Click **"Enable Cloud"**
7. ✅ You're live!

---

## 🎬 Usage Flow

### 👨‍💼 Admin Setup (5 minutes before event)

```
1. Settings → Change admin code to something secure
2. Setup → Add all judges (with PINs like 1234, 5678, etc.)
3. Setup → Add all contestants (names, numbers, categories)
4. Setup → Add rounds:
   - Interview (30%, 0-10 points)
   - Talent (40%, 0-10 points)
   - Evening Gown (30%, 0-10 points)
5. Share event code with all judges: "myevent2025"
```

### 👥 Judge Setup (1 minute each)

```
1. Open index.html on their device (phone/tablet/laptop)
2. Settings → Cloud Sync → Paste Firebase config
3. Enter event code: "myevent2025"
4. Click "Enable Cloud"
5. Login page → Enter name + PIN
6. Start scoring! 🎉
```

### 📊 During Event (Admin)

```
- Round Results tab → Monitor scores in real-time
- Final Results tab → See current standings
- Export CSV → Download results anytime
```

---

## 🔄 Typical Event Timeline

| Time | Action | Who |
|------|--------|-----|
| **Day before** | Setup Firebase, configure app | Admin |
| **1 hour before** | Add judges/contestants, test | Admin |
| **30 min before** | Judges enable cloud sync, test login | Judges |
| **Event starts** | Interview round scoring | All Judges |
| **Between rounds** | Admin checks Round Results | Admin |
| **Event continues** | Talent + Evening Gown rounds | All Judges |
| **Event ends** | View Final Results, export CSV | Admin |
| **After event** | Export JSON backup, export CSV | Admin |

---

## 💡 Event Code Examples

Choose a unique event code (share with judges/admins only):

✅ **Good Event Codes**:
- `gwf-seattle-2025`
- `missindia-wa-nov2025`
- `pageant-final-xk9m`
- `talent-show-2025-secure`

❌ **Bad Event Codes**:
- `test` (too common)
- `pageant` (too generic)
- `123` (too simple)

---

## 🎯 Device Recommendations

### Admin Workstation
- **Best**: Laptop with large screen
- **Why**: Need to view all data, export reports
- **Setup**: Full setup in Settings

### Judge Devices
- **Best**: Tablets or laptops
- **Good**: Large phones (6"+ screen)
- **Why**: Easy score entry, see multiple contestants
- **Setup**: Enable cloud sync, login with PIN

---

## 🚨 Common Issues & Fixes

### "Failed to enable cloud"
```
❌ Problem: Invalid Firebase config
✅ Fix: Copy the entire {...} object from Firebase Console
```

### Scores not syncing
```
❌ Problem: Different event codes
✅ Fix: Verify ALL devices use exact same event code (case-sensitive!)
```

### Judge can't login
```
❌ Problem: Wrong PIN
✅ Fix: Admin → Setup → Judges → Verify PIN is set correctly
```

### Data disappeared
```
❌ Problem: Cleared browser data
✅ Fix: Re-enable cloud sync → Data loads from Firestore
```

---

## 📱 Device Testing Checklist

Before the event, test with 2+ devices:

- [ ] Admin enables cloud sync on Device 1
- [ ] Admin adds test judge on Device 1
- [ ] Judge enables cloud sync on Device 2 (same event code!)
- [ ] Admin adds contestant on Device 1
- [ ] Verify contestant appears on Device 2 within seconds
- [ ] Judge enters test score on Device 2
- [ ] Verify score appears in Round Results on Device 1
- [ ] Both devices show same data ✅

---

## 💾 Backup Strategy

**During Event**:
- Export JSON every hour
- Keep exported files safe

**After Event**:
- Export final JSON (master backup)
- Export final CSV (for announcements)
- Download audit log CSV (for records)

**File Names**:
```
pageant_2025_backup_10am.json
pageant_2025_backup_12pm.json
pageant_2025_final.json
pageant_2025_results.csv
pageant_2025_audit.csv
```

---

## 🎓 Training Script for Judges

**Before Event (5 min per judge)**:

```
"Hi [Judge Name]!

1. Open this link: [your-github-pages-url]/index.html
   OR: Open the index.html file I sent you

2. Click 'Settings' tab at top

3. I'm going to paste something - click in the big text box
   [Admin pastes Firebase config]

4. Below that, type: myevent2025
   [Judge types event code]

5. Click 'Enable Cloud' button
   You should see: ✅ Cloud sync enabled!

6. Click 'Login' tab at top

7. Type your name: [Judge Name]
   Type your PIN: 1234
   [Each judge has unique PIN]

8. Click 'Sign In as Judge'

9. You'll see 'Scoring' page - perfect!

10. Select your name from dropdown (should be auto-selected)
    Select the round: Interview
    
11. For each contestant, enter score 0-10 in 'Score' column
    Add notes if needed
    Scores save automatically!

12. When done with round, click 'Submit Scores' button

That's it! Your scores sync to all devices instantly.
Any questions?"
```

---

## 📞 Day-of-Event Support

**Admin Should Know**:
- How to add/remove judges
- How to reset judge PINs
- How to export backups
- How to view Round/Final Results

**Have Ready**:
- Backup laptop with app loaded
- Firebase config copied somewhere safe
- Event code written down
- List of judge names + PINs

**Emergency Contacts**:
- Internet/WiFi support person
- Backup admin who knows the system

---

## 🎉 Success Checklist

Your event is ready when:

- [ ] Firebase project created & Firestore enabled
- [ ] Security rules updated
- [ ] Admin has Firebase config saved
- [ ] Event code chosen (unique & shared with team)
- [ ] All judges added with PINs
- [ ] All contestants added
- [ ] All rounds configured (weights = 100%)
- [ ] Tested with 2+ devices successfully
- [ ] All judges trained on scoring interface
- [ ] Backup plan ready (extra devices, internet)
- [ ] Export strategy planned (when to backup)

---

## 🚀 You're Ready!

Follow these steps, and you'll have a professional, real-time pageant scoring system with zero hosting costs and instant sync across all devices.

**Need more help?**
- See [FIRESTORE_SETUP.md](FIRESTORE_SETUP.md) for detailed Firebase instructions
- See [README.md](README.md) for complete feature documentation

**Good luck with your event! 🎊**
