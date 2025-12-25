# EchoBolt Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         USER BROWSER                             │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                    React Frontend                          │  │
│  │                  (http://localhost:5173)                   │  │
│  │                                                             │  │
│  │  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  │  │
│  │  │  Login   │  │ Register │  │   Home   │  │Playlists │  │  │
│  │  │  Page    │  │   Page   │  │   Page   │  │   Page   │  │  │
│  │  └──────────┘  └──────────┘  └──────────┘  └──────────┘  │  │
│  │                                                             │  │
│  │  ┌─────────────────────────────────────────────────────┐  │  │
│  │  │           Context API (AuthContext)                 │  │  │
│  │  │  - User state                                       │  │  │
│  │  │  - JWT token management                             │  │  │
│  │  │  - Login/Register/Logout functions                  │  │  │
│  │  └─────────────────────────────────────────────────────┘  │  │
│  │                                                             │  │
│  │  ┌─────────────────────────────────────────────────────┐  │  │
│  │  │           API Utils (Axios)                         │  │  │
│  │  │  - getAllSongs()                                    │  │  │
│  │  │  - uploadSong()                                     │  │  │
│  │  │  - createPlaylist()                                 │  │  │
│  │  │  - addSongToPlaylist()                              │  │  │
│  │  └─────────────────────────────────────────────────────┘  │  │
│  │                                                             │  │
│  │  ┌─────────────────────────────────────────────────────┐  │  │
│  │  │        Audio Player Component                       │  │  │
│  │  │  - HTML5 <audio> element                            │  │  │
│  │  │  - Play/Pause controls                              │  │  │
│  │  │  - Stream from backend                              │  │  │
│  │  └─────────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────────┘  │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            │ HTTP/HTTPS
                            │ REST API Calls
                            │
┌───────────────────────────▼─────────────────────────────────────┐
│                    Express Backend Server                        │
│                  (http://localhost:1337)                         │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                    API Routes                              │  │
│  │                                                             │  │
│  │  /api/v1/auth/         /api/v1/songs/      /api/v1/       │  │
│  │  ├─ register           ├─ GET /            playlist/       │  │
│  │  └─ login              ├─ POST /upload     ├─ create       │  │
│  │                        ├─ GET /stream/:fn  ├─ GET /        │  │
│  │                        └─ DELETE /:id      ├─ GET /:id     │  │
│  │                                            ├─ add/:id      │  │
│  │                                            ├─ remove/:id   │  │
│  │                                            └─ DELETE /:id  │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                    Middlewares                             │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐       │  │
│  │  │    CORS     │  │    Auth     │  │   Multer    │       │  │
│  │  │  Middleware │  │  Middleware │  │  (Upload)   │       │  │
│  │  └─────────────┘  └─────────────┘  └─────────────┘       │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                    Controllers                             │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │  │
│  │  │    Auth      │  │    Song      │  │   Playlist   │    │  │
│  │  │  Controller  │  │  Controller  │  │  Controller  │    │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘    │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                    Models (Mongoose)                       │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │  │
│  │  │     User     │  │     Song     │  │   Playlist   │    │  │
│  │  │    Model     │  │    Model     │  │    Model     │    │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘    │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                   │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                File Storage (uploads/)                     │  │
│  │  ┌──────────────────────────────────────────────────┐     │  │
│  │  │  Audio Files: .mp3, .wav, .ogg, .m4a, .flac       │     │  │
│  │  │  Stored with unique filenames                      │     │  │
│  │  │  Streamed via HTTP range requests                  │     │  │
│  │  └──────────────────────────────────────────────────┘     │  │
│  └───────────────────────────────────────────────────────────┘  │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            │ MongoDB Protocol
                            │
┌───────────────────────────▼─────────────────────────────────────┐
│                    MongoDB Database                              │
│                (mongodb://localhost:27017/echobolt)              │
│                                                                   │
│  ┌───────────────┐  ┌───────────────┐  ┌───────────────┐       │
│  │     users     │  │     songs     │  │   playlists   │       │
│  │  collection   │  │  collection   │  │  collection   │       │
│  │               │  │               │  │               │       │
│  │  - username   │  │  - title      │  │  - name       │       │
│  │  - email      │  │  - artist     │  │  - description│       │
│  │  - password   │  │  - filename   │  │  - songs[]    │       │
│  │  - createdAt  │  │  - uploadedBy │  │  - owner      │       │
│  │               │  │  - createdAt  │  │  - createdAt  │       │
│  └───────────────┘  └───────────────┘  └───────────────┘       │
└─────────────────────────────────────────────────────────────────┘

═══════════════════════════════════════════════════════════════════

                        DATA FLOW EXAMPLES

1. UPLOAD SONG:
   User → Upload Form → POST /api/v1/songs/upload (with file)
   → Auth Middleware (verify JWT) → Multer (save file)
   → Song Controller → Create Song in DB → Return success

2. PLAY SONG:
   User clicks Play → GET /api/v1/songs/stream/:filename
   → Song Controller → Stream file with range support
   → Browser Audio Element plays

3. CREATE PLAYLIST:
   User → Create Form → POST /api/v1/playlist/create
   → Auth Middleware → Playlist Controller
   → Create Playlist in DB → Return success

4. ADD SONG TO PLAYLIST:
   User → Select Playlist → POST /api/v1/playlist/add/:id
   → Auth Middleware → Playlist Controller
   → Update Playlist songs[] → Return updated playlist

═══════════════════════════════════════════════════════════════════

                    AUTHENTICATION FLOW

1. REGISTER:
   User Input → POST /api/v1/auth/register
   → Hash password (bcrypt) → Save user to DB
   → Generate JWT token → Return token + user

2. LOGIN:
   User Input → POST /api/v1/auth/login
   → Find user by email → Compare password (bcrypt)
   → Generate JWT token → Return token + user

3. AUTHENTICATED REQUEST:
   Request with JWT → Auth Middleware extracts token
   → Verify JWT signature → Decode user info
   → Attach user to req.user → Continue to controller

═══════════════════════════════════════════════════════════════════
```

## Technology Choices Explained

### Why MongoDB?
- Flexible schema for music metadata
- Easy to scale
- Good performance for read-heavy workloads
- Simple deployment (local or Atlas)

### Why JWT?
- Stateless authentication
- Works well with REST APIs
- Easy to implement
- Secure when properly configured

### Why React?
- Component-based architecture
- Large ecosystem
- Fast development
- Great developer experience

### Why Express?
- Minimalist and flexible
- Large middleware ecosystem
- Well-documented
- Industry standard

### Why Multer?
- Easy file upload handling
- Good documentation
- Flexible configuration
- Built for Express

## Security Layers

```
┌─────────────────────────────────────────┐
│  1. Input Validation                    │
│     - Email format                      │
│     - Password length                   │
│     - File type checking                │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│  2. Authentication                      │
│     - Password hashing (bcrypt)         │
│     - JWT token signing                 │
│     - Token verification                │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│  3. Authorization                       │
│     - User ownership checks             │
│     - Protected routes                  │
│     - Playlist access control           │
└─────────────────────────────────────────┘
              ↓
┌─────────────────────────────────────────┐
│  4. File Security                       │
│     - File type validation              │
│     - File size limits (50MB)           │
│     - Unique filenames                  │
└─────────────────────────────────────────┘
```
