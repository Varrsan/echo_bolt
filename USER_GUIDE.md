# User Guide - EchoBolt Music Platform

Welcome to EchoBolt! This guide will help you get started with the platform.

## 🚀 Getting Started

### First Time Setup

1. **Start the Backend**
   ```bash
   cd backend
   npm install
   cp .env.example .env
   # Edit .env with your MongoDB connection
   npm run dev
   ```

2. **Start the Frontend**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

3. **Open in Browser**
   - Navigate to http://localhost:5173

## 👤 Creating Your Account

1. Click "Register" on the login page
2. Fill in:
   - **Username**: Your display name
   - **Email**: Your email address
   - **Password**: At least 6 characters
   - **Confirm Password**: Must match
3. Click "Register"
4. You'll be automatically logged in!

## 🎵 Uploading Your First Song

1. Click the **"Upload Song"** button (green button in header)
2. Fill in the form:
   - **Title**: Name of the song
   - **Artist**: Artist or band name
   - **Audio File**: Select an audio file
     - Supported formats: MP3, WAV, OGG, M4A, FLAC
     - Max size: 50MB
3. Click **"Upload"**
4. Your song will appear in the list!

### Tips for Uploading
- ✅ Use clear, descriptive titles
- ✅ Include accurate artist names
- ✅ Compress large files if needed
- ✅ Ensure good audio quality

## ▶️ Playing Music

### Basic Playback

1. **Find a song** in the list
2. **Click the play button (▶)** next to any song
3. The song will start playing
4. **Click pause (⏸)** to pause

### Player Features

- **Currently Playing**: Shows at the top with song info
- **Auto-highlight**: Playing song is highlighted in blue
- **Easy switching**: Click play on any song to switch
- **Continuous play**: Player stays active while you browse

### Playback Controls

```
▶ Play    - Start playing a song
⏸ Pause   - Pause current song
```

## 📁 Creating Playlists

### Create a New Playlist

1. Click **"Create Playlist"** button (cyan button)
2. Enter:
   - **Playlist Name**: Give it a meaningful name
   - **Description** (optional): Notes about the playlist
3. Click **"Create"**

### Example Playlists
- "Workout Mix" - Energetic songs for exercise
- "Chill Vibes" - Relaxing music
- "Study Music" - Focus music
- "Party Playlist" - Upbeat songs

## ➕ Adding Songs to Playlists

### Method 1: From Home Page

1. Find the song you want to add
2. Click **"+ Playlist"** button next to it
3. A popup appears showing your playlists
4. Click on the playlist you want
5. Song is added! ✓

### Method 2: From Playlist View

1. Go to **"My Playlists"**
2. Select a playlist
3. Go back to Home
4. Add songs using the "+ Playlist" button

## 📋 Managing Playlists

### Viewing Your Playlists

1. Click **"My Playlists"** in the header
2. See all your playlists on the left
3. Click any playlist to view its songs

### Playing from Playlists

1. Open a playlist
2. Click **▶** on any song in the playlist
3. Songs play just like from the main library

### Removing Songs

1. Open the playlist
2. Find the song to remove
3. Click **"Remove"** button
4. Song is removed from playlist (but stays in library)

### Deleting Playlists

1. Find the playlist in the sidebar
2. Click **"Delete"** button on the playlist card
3. Confirm deletion
4. Playlist is removed (songs remain in library)

## 🗑️ Deleting Songs

### Who Can Delete?
- Only songs you uploaded can be deleted
- You cannot delete other users' songs

### How to Delete

1. Find your song in the list
2. Look for the **"Delete"** button (red)
3. Click **"Delete"**
4. Confirm the deletion
5. Song is permanently removed

**Warning**: Deleted songs cannot be recovered!

## 🔐 Account Management

### Logging Out

1. Click the **"Logout"** button (red) in the header
2. You'll be redirected to the login page
3. Your session is cleared

### Logging Back In

1. Enter your email and password
2. Click **"Login"**
3. You're back in!

### Session Management
- Your session persists across browser refreshes
- Sessions last 7 days
- Log out to clear your session

## 💡 Tips & Tricks

### Organization Tips
1. **Use descriptive playlist names** - Makes finding music easier
2. **Create themed playlists** - Group similar songs
3. **Add descriptions** - Remember what each playlist is for
4. **Regular cleanup** - Remove songs you don't listen to

### Upload Best Practices
1. **Check file format** - Use MP3 for compatibility
2. **Verify metadata** - Accurate title and artist
3. **Test playback** - Play after upload to verify
4. **Organize immediately** - Add to playlists right away

### Playlist Strategies
```
Personal Library Organization:
├── Favorites (top songs)
├── Recently Added (new discoveries)
├── By Mood
│   ├── Energetic
│   ├── Relaxed
│   └── Focus
└── By Genre
    ├── Rock
    ├── Pop
    └── Classical
```

## 🎨 User Interface Guide

### Home Page Layout

```
┌─────────────────────────────────────────────┐
│ 🎵 EchoBolt Music    [Upload] [Create] [...] │
├─────────────────────────────────────────────┤
│                                              │
│ Currently Playing: Song Name - Artist       │
│                              [⏸ Pause]       │
├─────────────────────────────────────────────┤
│                                              │
│ All Songs                                   │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │ Song 1 - Artist 1    [▶] [+] [Delete]  │ │
│ │ Song 2 - Artist 2    [▶] [+]           │ │
│ │ Song 3 - Artist 3    [▶] [+] [Delete]  │ │
│ └─────────────────────────────────────────┘ │
└─────────────────────────────────────────────┘
```

### Playlist Page Layout

```
┌─────────────────────────────────────────────┐
│ 📁 My Playlists           [Back to Home]    │
├─────────────────────────────────────────────┤
│                                              │
│ Playlists          │ Playlist: "Favorites"  │
│ ─────────────────  │ ────────────────────── │
│ > Favorites        │ Song 1   [▶] [Remove]  │
│   Workout Mix      │ Song 2   [▶] [Remove]  │
│   Chill Vibes      │ Song 3   [▶] [Remove]  │
│                    │                         │
└─────────────────────────────────────────────┘
```

## ⚡ Keyboard Shortcuts

While we don't have keyboard shortcuts yet, here are planned features:
- Space: Play/Pause
- N: Next song
- P: Previous song
- M: Mute

## 🐛 Troubleshooting

### Song won't play?
- Check file format is supported
- Ensure backend is running
- Try refreshing the page

### Upload failed?
- Check file size (max 50MB)
- Verify file format
- Ensure you're logged in
- Check backend connection

### Can't see my playlists?
- Make sure you're logged in
- Try refreshing the page
- Check that you created playlists

### Login issues?
- Verify email and password
- Check if backend is running
- Clear browser cache

## 📱 Mobile Usage

The platform works on mobile browsers:
- Touch-friendly buttons
- Responsive layout
- Mobile audio support

**Note**: Desktop experience is recommended for uploading.

## 🎯 Common Workflows

### Daily Listening
1. Login
2. Go to playlists
3. Select your daily playlist
4. Hit play and enjoy!

### Adding New Music
1. Upload new songs
2. Test playback
3. Add to appropriate playlists
4. Organize and enjoy

### Playlist Curation
1. Browse all songs
2. Create themed playlist
3. Add relevant songs
4. Fine-tune by removing/adding
5. Enjoy your curated collection

## 🌟 Pro Tips

1. **Batch Upload**: Upload multiple songs at once
2. **Playlist First**: Create playlists before uploading
3. **Consistent Naming**: Use consistent naming conventions
4. **Regular Cleanup**: Remove old songs you don't need
5. **Backup Important**: Keep backup of important audio files

## 🎊 Enjoy Your Music!

That's it! You're ready to use EchoBolt like a pro. 

Happy listening! 🎵

---

**Need help?** Check:
- [README.md](README.md) - Technical documentation
- [SETUP.md](SETUP.md) - Setup instructions
- [API_TESTING.md](API_TESTING.md) - API reference
