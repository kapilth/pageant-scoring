# Admin-Only Controls Implementation

## Overview
The pageant scoring app now restricts certain features to admin users only:
- **Export JSON/CSV buttons** - Only admins can download scores
- **Import JSON button** - Only admins can import data
- **Reset All button** - Only admins can clear all data
- **Developer Tools section** - Only admins can view raw state data

## How It Works

### Role-Based Access
- **Admin Role**: Full access to all features including exports and developer tools
- **Judge Role**: Can only access scoring interface, no data export/import capabilities

### Implementation Details

1. **Dynamic Admin Controls** (Line 56)
   - Header contains `<div id="adminControls"></div>` that gets populated only for admins
   - Buttons are dynamically created based on user role

2. **Named Functions** (Lines 630-664)
   - `exportJson()` - Export state as JSON file
   - `exportCsv()` - Export all scores as CSV file
   - `resetApp()` - Clear all local data and reload
   - `importJson()` - Import data from JSON file

3. **updateAdminControls() Function** (Lines 159-183)
   - Called automatically during `render()`
   - Checks if `state.me.role === 'admin'`
   - Shows/hides admin controls and developer tools accordingly
   - Wires up event handlers to named functions

4. **Developer Tools Section** (Line 66)
   - Hidden by default: `style="display:none"`
   - Only shown when user role is admin
   - Displays raw JSON state for debugging

## Testing

### As Admin
1. Sign in as Admin (code: ADMIN123)
2. You should see: Export JSON, Export CSV, Import JSON, Reset All buttons in header
3. Developer Tools section should be visible at bottom of Settings tab

### As Judge
1. Sign in as Judge with a judge PIN
2. Header should be empty (no export/import/reset buttons)
3. Developer Tools section should be hidden
4. Can only access Scoring tab

## Security Notes
- This is **client-side access control** only
- Data is still accessible in browser localStorage and Firestore
- For production use, implement Firestore Security Rules to restrict data access server-side
- Judge users cannot export data through the UI, but technically could access it via browser dev tools

## Firestore Security Rules (Recommended)
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /events/{eventCode} {
      // Only allow reads - no user authentication implemented
      allow read: if true;
      
      // In production, restrict writes based on authentication
      allow write: if false;
    }
  }
}
```

## Future Enhancements
- Implement Firebase Authentication for proper user management
- Add server-side validation for admin operations
- Add audit logging for all admin actions
- Implement role-based Firestore security rules
