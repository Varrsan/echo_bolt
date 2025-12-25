# Quick Start Guide

Get EchoBolt up and running in 5 minutes!

## 🚀 Quick Setup

### 1. Prerequisites
- Node.js (v14+)
- MongoDB (local or Atlas)

### 2. Backend

```bash
cd backend
npm install
cp .env.example .env
# Edit .env and set MONGO_URI and JWT_SECRET
npm run dev
```

### 3. Frontend

```bash
cd frontend
npm install
npm run dev
```

### 4. Access

Open http://localhost:5173 in your browser!

## 🎵 Quick Start Actions

1. **Register** - Create your account
2. **Upload** - Add your first song
3. **Play** - Enjoy the music!
4. **Playlist** - Organize your favorites

## 📚 Need More Help?

- See [SETUP.md](SETUP.md) for detailed instructions
- See [README.md](README.md) for full documentation

## 🐛 Common Issues

**Can't connect to backend?**
- Ensure MongoDB is running
- Check backend is on port 1337
- Verify .env configuration

**Upload not working?**
- Check file format (MP3, WAV, OGG, M4A, FLAC)
- Ensure file size < 50MB
- Verify you're logged in

---

**Enjoy your music! 🎶**
