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
- User registration and authentication (JWT-based)
- Upload, stream, and delete songs (audio files)
- Create, view, and delete playlists
- Add or remove songs from playlists
- Explore and stream all available songs
- Responsive, modern UI with React and Tailwind CSS

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

1. **Install dependencies:**
   ```bash
   cd backend
   npm install
   ```
2. **Create a `.env` file** in `backend/` with the following variables:
   ```env
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   ```
3. **Start the backend server:**
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
2. **Start the frontend dev server:**
   ```bash
   npm run dev
   ```
   The frontend runs on [http://localhost:5173](http://localhost:5173) by default (Vite).

---

## API Overview

### Auth
- `POST /api/v1/auth/register` — Register a new user
- `POST /api/v1/auth/login` — Login and receive JWT

### Songs
- `POST /api/v1/song/upload` — Upload a new song (auth required)
- `GET /api/v1/songs` — List all songs
- `GET /api/v1/stream/:filename` — Stream a song by filename
- `DELETE /api/v1/song/delete/:id` — Delete a song (auth required)

### Playlists
- `POST /api/v1/playlist/create` — Create a new playlist (auth required)
- `GET /api/v1/playlist/` — List all playlists for the user
- `GET /api/v1/playlist/:id` — Get a specific playlist
- `POST /api/v1/playlist/add/:id` — Add a song to a playlist
- `DELETE /api/v1/playlist/remove/:id` — Remove a song from a playlist
- `DELETE /api/v1/playlist/delete/:id` — Delete a playlist

---

## Environment Variables
Both backend and frontend expect a `.env` file for sensitive configuration. At minimum, set:
- `MONGO_URI` (backend)
- `JWT_SECRET` (backend)

---
