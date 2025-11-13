# Pageant Scoring App

A professional, real-time scoring application for pageants, talent shows, and judged competitions. Features cloud sync via Google Firestore, multi-judge scoring, weighted rounds, and comprehensive reporting.

![Version](https://img.shields.io/badge/version-2.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)

## ✨ Features

### 🔐 User Management
- **Dual Login System**: Separate Admin and Judge roles
- **PIN-based Judge Authentication**: Secure judge login with unique PINs
- **Role-based Access Control**: Different interfaces for admins and judges

### ⚙️ Event Setup (Admin)
- Manage judges with PIN codes
- Add contestants with numbers and categories
- Configure multiple scoring rounds (Talent, Interview, Evening Gown, etc.)
- Set custom weights and max points per round (0-10 scale)
- Automatic weight normalization

### 📊 Scoring System
- Real-time score entry with auto-save
- Judge-locked scoring (prevents cross-contamination)
- Optional notes/comments per score
- Score validation and clamping
- Score aggregation (average or sum)

### 📈 Results & Reporting
- **Round Results**: View and sort scores by round
- **Final Results**: Weighted calculations across all rounds
- **Export Options**: JSON and CSV exports
- **Sorting**: By score, contestant number, or name

### ☁️ Cloud Sync (Firestore)
- **Real-time synchronization** across all devices
- **Offline support** with automatic sync when online
- **Multi-device collaboration** using shared event codes
- **No server required** - Google hosts everything
- **Free tier** suitable for most events

### 📝 Audit Trail
- Complete audit log of all actions
- User attribution and timestamps
- Detailed change tracking
- Export audit logs to CSV

### 📱 Progressive Web App (PWA)
- Installable on any device
- Works offline
- Responsive design (mobile + desktop)
- Professional dark theme

## 🚀 Quick Start

### Option 1: Local Use (No Setup Required)

1. **Download** `index.html` to your computer
2. **Open** it in any modern web browser
3. **Sign in** as Admin (default code: `ADMIN123`)
4. **Start** adding judges, contestants, and rounds!

### Option 2: Cloud Sync (Recommended for Multi-Device)

1. Follow steps from **Option 1** first
2. **Set up Firestore** - See [FIRESTORE_SETUP.md](FIRESTORE_SETUP.md)
3. In the app: **Settings** → **Cloud Sync**
4. Paste Firebase config and enter event code
5. **Share** event code with all judges/admins
6. **Enjoy** real-time sync across all devices!

### Option 3: Host on GitHub Pages (Free)

1. Fork or clone this repository
2. Go to **Settings** → **Pages**
3. Set source to `main` branch
4. Your app will be live at `https://yourusername.github.io/pageant-scoring`

## 📖 Usage Guide

### Admin Workflow

1. **Login** as Admin (Settings tab to change default code)
2. **Setup Event**:
   - Add all judges (assign unique PINs)
   - Add all contestants (with numbers and categories)
   - Create rounds (set names, types, weights, max points)
3. **Enable Cloud Sync** (Settings tab) if using multiple devices
4. **Share** event code with judges
5. **Monitor** scoring progress (Round Results tab)
6. **View** final results (Final Results tab)
7. **Export** results to CSV

### Judge Workflow

1. **Login** with your name and PIN code (from admin)
2. **Choose** judge (auto-locked to your profile) and round
3. **Enter scores** for each contestant (0-10 scale)
4. **Add notes** (optional)
5. Scores **auto-save** as you type
6. Click **Submit Scores** when round is complete

### Scoring Example

**Event**: Mrs. India Washington 2025

**Rounds**:
- Interview (30% weight, 0-10 points)
- Talent (40% weight, 0-10 points)
- Evening Gown (30% weight, 0-10 points)

**Judges**: 5 judges, each scores all contestants

**Final Score Calculation**:
```
For each contestant:
  Interview Score = average of 5 judges' scores
  Talent Score = average of 5 judges' scores
  Evening Gown Score = average of 5 judges' scores
  
  Final = (Interview × 0.30) + (Talent × 0.40) + (Evening Gown × 0.30)
```

Contestants ranked by final weighted score (highest first).

## 🛠️ Technical Details

### Built With
- **Pure HTML/CSS/JavaScript** - No build tools, no dependencies
- **Firebase SDK** - For Firestore cloud sync
- **Service Worker** - For offline PWA functionality
- **localStorage** - Local data persistence

### Browser Support
- ✅ Chrome/Edge (recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

### Data Storage
- **Local**: Browser localStorage (JSON)
- **Cloud**: Google Firestore (NoSQL database)
- **Exports**: JSON and CSV files

### File Structure
```
pageant-scoring/
├── index.html              # Main app (all-in-one file)
├── index_new.html          # Variant with Firebase
├── index_old.html          # Variant with additional features
├── index_v2.html           # Latest variant
├── README.md               # This file
└── FIRESTORE_SETUP.md      # Firestore setup guide
```

## 🔒 Security Notes

### Default Admin Code
- Default: `ADMIN123`
- **Change immediately** in Settings tab for production use
- Stored locally in browser

### Judge PINs
- Set by admin in Setup → Judges
- Required for judge login
- Can be simple (e.g., `1234`) for informal events
- Use longer codes (e.g., `7429`) for formal events

### Firestore Security
- Current setup: Anyone with event code can read/write
- Event code acts as a shared password
- Perfect for controlled pageant events
- For public events, consider Firebase Authentication (see FIRESTORE_SETUP.md)

### Data Privacy
- All data stored locally in browser + Firestore
- No external analytics or tracking
- You control the Firebase project
- Export and delete data anytime

## 📊 Data Export Formats

### JSON Export
Complete app state for backup/restore:
```json
{
  "judges": [...],
  "contestants": [...],
  "rounds": [...],
  "scores": {...},
  "audit": [...]
}
```

### CSV Exports

**All Scores Export**:
```csv
Judge,Contestant #,Contestant,Category,Round,Sub,Score,Notes
Judge Sarah,1,Jane Doe,Mrs. India WA,Talent,,9.5,Excellent performance
...
```

**Round Results Export**:
```csv
Contestant #,Name,Category,Score (average),Judges Count
1,Jane Doe,Mrs. India WA,9.2,5
...
```

**Final Results Export**:
```csv
Contestant #,Name,Category,Interview,Talent,Evening Gown,Total (weighted)
1,Jane Doe,Mrs. India WA,27.6,36.8,27.3,91.7
...
```

## 🎯 Use Cases

- 🎭 **Pageants**: Beauty pageants, talent competitions
- 🏆 **Competitions**: Science fairs, art contests, hackathons
- 🎤 **Talent Shows**: School shows, community events
- 🥋 **Sports**: Gymnastics, figure skating, diving
- 🎨 **Judged Events**: Any event with multiple judges and rounds

## 🤝 Contributing

This is a single-file app designed for simplicity. Contributions welcome:

1. Fork the repository
2. Create a feature branch
3. Make your changes to `index.html`
4. Test thoroughly
5. Submit a pull request

## 📄 License

MIT License - feel free to use for any purpose, commercial or personal.

## 💡 Tips & Tricks

### Best Practices
- ✅ **Test first**: Run a test event with sample data before the real event
- ✅ **Export backups**: Use Export JSON regularly during the event
- ✅ **Strong event code**: Use unique event codes like `gwf-2025-xk9m`
- ✅ **Brief judges**: Show judges the scoring interface before the event
- ✅ **Verify weights**: Make sure round weights total 100%

### Troubleshooting
- **Scores not syncing?** Check internet connection and event code
- **Judge locked out?** Admin can reset judge PIN in Setup
- **Data lost?** Import from JSON backup or restore from Firestore
- **Weights don't add to 100%?** App auto-normalizes, but fix for clarity

### Advanced Features
- Use **sub-rounds** for complex scoring (e.g., Swimsuit → Preliminary vs Final)
- Set different **max points** per round (0-5 for interview, 0-10 for talent)
- Enable **sum aggregation** instead of average for cumulative scoring
- Use **audit log** to trace any data discrepancies

## 📞 Support

For issues or questions:
- Check [FIRESTORE_SETUP.md](FIRESTORE_SETUP.md) for cloud sync issues
- Review browser console (F12) for error messages
- Ensure using modern browser (Chrome/Edge recommended)

## 🙏 Acknowledgments

Built for pageant organizers who need a simple, reliable, real-time scoring solution without the complexity of traditional scoring software.

---

**Made with ❤️ for pageant organizers everywhere**
