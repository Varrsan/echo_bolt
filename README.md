# EchoBolt Music Streaming App

EchoBolt is a full-stack music streaming web application that allows users to register, upload, stream, and manage songs and playlists. The project is divided into two main parts: a Node.js/Express backend and a React frontend.

---

## Table of Contents
- [Features](#features)
- [Project Structure](#project-structure)
- [Backend Setup](#backend-setup)
- [Frontend Setup](#frontend-setup)
- [API Overview](#api-overview)
- [Environment Variables](#environment-variables)
- [License](#license)

---

## Features
- 🎵 **Music Streaming**: Upload and stream audio files (MP3, WAV, OGG, M4A, FLAC)
- 🔐 **User Authentication**: Secure JWT-based registration and login
- ▶️ **Music Player**: Play and pause songs with an integrated audio player
- 📤 **Upload Songs**: Upload your favorite music with title and artist information
- 📁 **Playlists**: Create, manage, and organize songs into custom playlists
- ➕ **Playlist Management**: Add or remove songs from playlists
- 🗑️ **Delete Songs**: Remove your uploaded songs
- 👥 **Multi-user Support**: Each user has their own playlists
- 📱 **Responsive UI**: Clean, modern interface that works on all devices

---

## Project Structure
```
.
├── backend/         # Node.js/Express backend (API, DB, Auth, File Upload)
│   ├── config/      # Database connection
│   ├── controllers/ # API controllers (auth, songs, playlists)
│   ├── middlewares/ # Auth middleware
│   ├── models/      # Mongoose schemas
│   ├── routes/      # Express routes
│   ├── uploads/     # Uploaded audio files (GridFS)
│   ├── server.js    # Main server file
│   └── ...
├── frontend/        # React frontend (UI, pages, components)
│   ├── public/      # Static assets
│   ├── src/         # Source code
│   │   ├── pages/   # Main pages (Home, Login, Register, Songs, Playlist, etc.)
│   │   ├── components/ # UI components
│   │   ├── Context/ # React context providers
│   │   └── ...
│   └── ...
└── README.md        # Project documentation
```

---

## Backend Setup

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local installation or MongoDB Atlas account)

### Installation

1. **Install dependencies:**
   ```bash
   cd backend
   npm install
   ```

2. **Set up MongoDB:**
   - **Option 1: Local MongoDB**
     - Install MongoDB Community Edition from [mongodb.com](https://www.mongodb.com/try/download/community)
     - Start MongoDB service:
       ```bash
       # On Linux/Mac
       sudo systemctl start mongod
       # Or
       mongod --dbpath /path/to/data/directory
       ```
   
   - **Option 2: MongoDB Atlas (Cloud)**
     - Create a free account at [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
     - Create a new cluster
     - Get your connection string from the "Connect" button

3. **Create a `.env` file** in `backend/` directory:
   ```env
   MONGO_URI=mongodb://localhost:27017/echobolt
   # Or for MongoDB Atlas:
   # MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/echobolt
   
   JWT_SECRET=your_super_secret_jwt_key_here_change_this
   PORT=1337
   ```
   
   **Important:** Change the `JWT_SECRET` to a random, secure string!

4. **Start the backend server:**
   ```bash
   npm start
   # or for development with auto-reload
   npm run dev
   ```
   The backend runs on [http://localhost:1337](http://localhost:1337) by default.

---

## Frontend Setup

1. **Install dependencies:**
   ```bash
   cd frontend
   npm install
   ```

2. **Configure API URL (optional):**
   The frontend is configured to connect to the backend at `http://localhost:1337/api/v1` by default.
   If your backend runs on a different URL, update the `API_URL` constant in:
   - `frontend/src/context/AuthContext.jsx` (search for "API_URL")
   - `frontend/src/utils/api.js` (search for "API_URL")

3. **Start the frontend dev server:**
   ```bash
   npm run dev
   ```
   The frontend runs on [http://localhost:5173](http://localhost:5173) by default (Vite).

4. **Open your browser:**
   Navigate to [http://localhost:5173](http://localhost:5173) to use the application!

---

## API Overview

### Auth
- `POST /api/v1/auth/register` — Register a new user
- `POST /api/v1/auth/login` — Login and receive JWT

### Songs
- `POST /api/v1/songs/upload` — Upload a new song (auth required, multipart/form-data)
- `GET /api/v1/songs` — List all songs
- `GET /api/v1/songs/stream/:filename` — Stream a song by filename
- `DELETE /api/v1/songs/:id` — Delete a song (auth required)

### Playlists
- `POST /api/v1/playlist/create` — Create a new playlist (auth required)
- `GET /api/v1/playlist/` — List all playlists for the authenticated user
- `GET /api/v1/playlist/:id` — Get a specific playlist with all songs
- `POST /api/v1/playlist/add/:id` — Add a song to a playlist (auth required)
- `DELETE /api/v1/playlist/remove/:id` — Remove a song from a playlist (auth required)
- `DELETE /api/v1/playlist/:id` — Delete a playlist (auth required)

---

## Usage Guide

### Getting Started

1. **Register an Account**
   - Navigate to the register page
   - Create an account with username, email, and password
   - You'll be automatically logged in after registration

2. **Upload Songs**
   - Click the "Upload Song" button on the home page
   - Fill in the song title and artist name
   - Select an audio file (MP3, WAV, OGG, M4A, or FLAC)
   - Click "Upload" to add the song to the platform

3. **Play Music**
   - Browse all available songs on the home page
   - Click the play button (▶) on any song to start playing
   - The currently playing song will be highlighted
   - Use the pause button (⏸) to pause playback

4. **Create Playlists**
   - Click "Create Playlist" button
   - Enter a playlist name and optional description
   - Your playlist will be created and ready for songs

5. **Manage Playlists**
   - Click "+ Playlist" next to any song to add it to a playlist
   - Navigate to "My Playlists" to view all your playlists
   - Click on a playlist to see its songs
   - Play songs directly from playlists
   - Remove songs from playlists or delete entire playlists

### Features in Detail

**Authentication**: All user sessions are secured with JWT tokens. Tokens are stored in localStorage and automatically included in API requests.

**File Storage**: Audio files are stored on the server's filesystem in the `backend/uploads` directory.

**Streaming**: Songs are streamed using HTTP range requests, allowing for efficient playback and seeking.

**Authorization**: Users can only delete songs they uploaded and manage their own playlists.

---

## Environment Variables

### Backend (.env file in backend/)
```env
# MongoDB Connection
MONGO_URI=mongodb://localhost:27017/echobolt
# For MongoDB Atlas, use:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/echobolt

# JWT Secret (change this to a random string!)
JWT_SECRET=your_super_secret_jwt_key_here

# Server Port (optional, defaults to 1337)
PORT=1337
```

### Frontend
The frontend uses hardcoded API URLs. If you need to change the backend URL:
- Edit the `API_URL` constant in `frontend/src/context/AuthContext.jsx`
- Edit the `API_URL` constant in `frontend/src/utils/api.js`

---

## Technology Stack

### Backend
- **Node.js** - Runtime environment
- **Express.js** - Web framework
- **MongoDB** - Database
- **Mongoose** - ODM for MongoDB
- **JWT** - Authentication
- **Multer** - File upload handling
- **bcryptjs** - Password hashing

### Frontend
- **React** - UI library
- **Vite** - Build tool and dev server
- **React Router** - Navigation
- **Axios** - HTTP client
- **Context API** - State management

---

## Security Notes

- Always change the `JWT_SECRET` in production
- Use HTTPS in production environments
- Implement rate limiting for API endpoints in production
- Validate and sanitize all user inputs
- Store uploaded files securely with proper permissions
- Consider implementing file size limits and virus scanning for uploads

---
