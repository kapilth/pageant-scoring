# Firestore Security Implementation Guide

## Current Security Status

⚠️ **Important Security Information:**

The Firebase API key in the config is **NOT a secret**. It's designed to be public and is included in every Firebase web app. The API key just identifies your Firebase project - it doesn't grant access to data.

**Real security comes from Firestore Security Rules** (server-side), not hiding the API key.

## Current Risk Level: MEDIUM

### What's Protected:
✅ Firestore Security Rules prevent unauthorized access
✅ Each event has a unique event code (like a password)
✅ Audit logs are append-only (cannot be modified/deleted)

### What's NOT Protected:
❌ Anyone who knows the event code can read/write data
❌ No user authentication - just event code
❌ Anyone can see the source code and API key (but that's normal for web apps)

## Security Options

### Option 1: Current Setup (Simple, Medium Security)
**How it works:**
- Event code acts as a shared password
- Anyone with the event code can access that event's data
- Good for: Small events, trusted participants

**To implement:**
1. Go to [Firebase Console](https://console.firebase.google.com/project/womenfestival2025/firestore/rules)
2. Copy the rules from `firestore.rules` file
3. Publish the rules

### Option 2: Add Password Protection (Better Security)
**How it works:**
- Event has both a code AND a password
- Password is stored hashed in Firestore
- Users must enter password to access event

**Implementation:**
Would require adding password verification before allowing access.

### Option 3: Firebase Authentication (Best Security)
**How it works:**
- Each judge/admin has a Firebase account
- Real authentication with email/password
- Fine-grained permissions (read-only judges, admin rights)

**Implementation:**
Would require significant changes to add Firebase Auth.

## Recommended Approach for Your Use Case

For a pageant scoring app, I recommend **Option 1** with the following practices:

### Best Practices:

1. **Unique Event Codes**: Use hard-to-guess event codes
   - Good: `pageant2025-gWf7kX2`
   - Bad: `pageant2025`

2. **Change After Event**: Create new event code for each pageant

3. **Monitor Access**: Check audit logs regularly for suspicious activity

4. **Firestore Security Rules**: Deploy the rules from `firestore.rules`

5. **Limited Time**: Only enable cloud sync during the actual event

## What About Someone Accessing the Code?

**Yes, anyone can:**
- See the Firebase API key (this is normal and expected)
- See the source code (this is how all web apps work)
- Read the event code if they're already using the app

**No, they cannot (with proper security rules):**
- Access other events' data without the event code
- Modify audit logs (append-only)
- Access the Firebase Console (requires separate login)
- Delete your Firebase project

## Deploy Security Rules

### Step 1: Go to Firebase Console
Visit: https://console.firebase.google.com/project/womenfestival2025/firestore/rules

### Step 2: Copy Rules
Copy the contents of `firestore.rules` file

### Step 3: Publish
Click "Publish" to activate the rules

## Additional Security Layers

If you need stronger security, consider:

1. **Admin-Only Setup**: 
   - Only admins can create events
   - Judges get read-only access with PIN

2. **Time-Limited Access**:
   - Events automatically close after the pageant date

3. **IP Restrictions**:
   - Only allow access from event venue IP (enterprise feature)

4. **Audit Monitoring**:
   - Set up Firebase Cloud Functions to alert on suspicious activity

## Questions?

- Is the API key a secret? **No, it's meant to be public**
- Can someone hack my data? **Not without the event code + proper security rules**
- Should I hide the source code? **No, security through obscurity doesn't work**
- What's the weakest point? **The event code - make it strong and unique**

## Summary

Your data is as secure as:
1. Your event code strength (make it complex)
2. Your Firestore Security Rules (deploy them!)
3. Who you share the event code with (only trusted users)

For a single-event pageant app, this level of security is **appropriate and industry-standard**.
