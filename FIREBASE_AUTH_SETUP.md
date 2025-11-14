# Firebase Authentication Setup for Admin Access

## Overview
Admin access is now secured using Firebase Authentication. This provides proper security with encrypted passwords and secure authentication.

## Setting Up Admin Accounts

### 1. Access Firebase Console
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project: **womenfestival2025**
3. Navigate to **Authentication** in the left sidebar

### 2. Enable Email/Password Authentication
1. Click on the **Sign-in method** tab
2. Find **Email/Password** in the providers list
3. Click to enable it
4. Save changes

### 3. Create Admin User Accounts
1. Go to the **Users** tab in Authentication
2. Click **Add user**
3. Enter:
   - **Email**: Admin's email address (e.g., `admin@pageant2025.com`)
   - **Password**: A strong, secure password
4. Click **Add user**
5. Share credentials securely with the admin

### 4. Admin Login Process
Admins will:
1. Visit the app login page
2. Connect to the event using the event code
3. Enter their Firebase email and password in the Admin Login section
4. Click "Sign In as Admin"

## Security Benefits

✅ **Encrypted Passwords**: Passwords are never stored in plain text  
✅ **Secure Authentication**: Uses Firebase's industry-standard auth  
✅ **No Hard-coded Passwords**: Default password removed from source code  
✅ **Session Management**: Automatic session handling and persistence  
✅ **Audit Trail**: All admin logins are logged  

## Important Notes

- **Event Code Required**: Admins must connect to an event first before logging in
- **Firebase Project**: Uses the `womenfestival2025` Firebase project
- **Multiple Admins**: You can create multiple admin accounts as needed
- **Password Reset**: Use Firebase Console to reset admin passwords if needed

## Troubleshooting

### "Please connect to an event first"
- Make sure to enter the event code and click "Connect" before attempting admin login

### "No account found with this email"
- Admin account needs to be created in Firebase Console first

### "Incorrect password"
- Double-check the password or reset it via Firebase Console

### "Too many failed attempts"
- Firebase temporarily blocks repeated failed login attempts for security
- Wait a few minutes before trying again

## Creating Admin Accounts (Step-by-Step)

```
1. Firebase Console → Authentication → Users → Add user
2. Email: admin@example.com
3. Password: [strong password]
4. Click "Add user"
5. Share credentials with admin via secure channel (not email/SMS)
```

## Best Practices

1. **Use Strong Passwords**: Minimum 12 characters with mix of letters, numbers, symbols
2. **Unique Emails**: Each admin should have their own account
3. **Secure Sharing**: Share credentials via secure channel (password manager, in-person)
4. **Regular Review**: Periodically review admin accounts and remove unused ones
5. **Enable 2FA**: Consider enabling two-factor authentication for extra security (available in Firebase)
