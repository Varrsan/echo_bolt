# EchoBolt Setup Guide

This guide will walk you through setting up the EchoBolt music streaming platform from scratch.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v14 or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js)
- **MongoDB** - Choose one option:
  - Local installation - [Download](https://www.mongodb.com/try/download/community)
  - MongoDB Atlas (free cloud database) - [Sign up](https://www.mongodb.com/cloud/atlas)

## Step-by-Step Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Varrsan/echo_bolt.git
cd echo_bolt
```

### 2. Backend Setup

#### Install Dependencies

```bash
cd backend
npm install
```

#### Configure MongoDB

**Option A: Local MongoDB**

1. Install MongoDB Community Edition
2. Start MongoDB:
   ```bash
   # On Linux
   sudo systemctl start mongod
   
   # On macOS
   brew services start mongodb-community
   
   # On Windows
   # MongoDB runs as a service after installation
   
   # Or manually:
   mongod --dbpath /path/to/your/data/directory
   ```

**Option B: MongoDB Atlas (Recommended for beginners)**

1. Go to [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Sign up for a free account
3. Create a new cluster (free tier available)
4. Click "Connect" on your cluster
5. Choose "Connect your application"
6. Copy the connection string

#### Create Environment File

Create a `.env` file in the `backend` directory:

```bash
cp .env.example .env
```

Edit the `.env` file with your configuration:

```env
# For local MongoDB
MONGO_URI=mongodb://localhost:27017/echobolt

# For MongoDB Atlas (replace with your connection string)
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/echobolt

# Generate a random secret key for JWT
JWT_SECRET=your_super_secret_random_key_change_this_in_production

# Port (optional, defaults to 1337)
PORT=1337
```

**Important:** Generate a secure random string for `JWT_SECRET`. You can use:
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

#### Start the Backend

```bash
# Development mode (with auto-reload)
npm run dev

# Or production mode
npm start
```

You should see:
```
Server running on port 1337
MongoDB connected successfully
```

#### Test the Backend

Open your browser or use curl to test:
```bash
curl http://localhost:1337
# Should return: {"message":"EchoBolt API is running"}
```

### 3. Frontend Setup

Open a new terminal window (keep the backend running).

#### Install Dependencies

```bash
cd frontend
npm install
```

#### Configure API URL (Optional)

The frontend is configured to connect to the backend at `http://localhost:1337/api/v1` by default.

If your backend runs on a different URL, update the `API_URL` constant in:
- `frontend/src/context/AuthContext.jsx` (search for "API_URL")
- `frontend/src/utils/api.js` (search for "API_URL")

#### Start the Frontend

```bash
npm run dev
```

You should see:
```
  VITE v5.x.x  ready in xxx ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
```

### 4. Access the Application

Open your browser and navigate to:
```
http://localhost:5173
```

## First Steps

1. **Register**: Click "Register" and create an account
2. **Upload a Song**: Click "Upload Song" and add an audio file
3. **Play Music**: Click the play button on any song
4. **Create Playlist**: Click "Create Playlist" and organize your songs

## Troubleshooting

### Backend Issues

**Problem: "MongoDB connection error"**
- Ensure MongoDB is running
- Check your `MONGO_URI` in `.env`
- For Atlas, ensure your IP is whitelisted

**Problem: "Port 1337 already in use"**
- Change the `PORT` in `.env` to a different number
- Or stop the process using port 1337

**Problem: "JWT must be provided"**
- Ensure you have set `JWT_SECRET` in `.env`

### Frontend Issues

**Problem: "Network Error" or "Cannot connect to API"**
- Ensure backend is running on port 1337
- Check browser console for CORS errors
- Verify API URL in frontend configuration

**Problem: "Module not found"**
- Run `npm install` again in the frontend directory
- Delete `node_modules` and `package-lock.json`, then run `npm install`

### Upload Issues

**Problem: "File too large"**
- Maximum file size is 50MB
- Compress your audio files if needed

**Problem: "Only audio files are allowed"**
- Ensure file has extension: .mp3, .wav, .ogg, .m4a, or .flac

## Development Tips

### Backend Development

- Use `npm run dev` for auto-reload on code changes
- Backend logs all requests and errors to console
- Files are stored in `backend/uploads/`

### Frontend Development

- Vite provides hot module replacement (HMR)
- React DevTools browser extension is helpful
- Check browser console for errors

### Testing API Endpoints

Use tools like:
- **Postman** - [Download](https://www.postman.com/downloads/)
- **curl** (command line)
- **httpie** (command line)

Example API test:
```bash
# Register a user
curl -X POST http://localhost:1337/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"testuser","email":"test@example.com","password":"password123"}'

# Login
curl -X POST http://localhost:1337/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password123"}'

# Get all songs
curl http://localhost:1337/api/v1/songs
```

## Production Deployment

When deploying to production:

1. **Environment Variables**: Use secure values for `JWT_SECRET`
2. **Database**: Use MongoDB Atlas or a secure MongoDB instance
3. **HTTPS**: Enable SSL/TLS
4. **CORS**: Configure CORS for your production domain
5. **File Storage**: Consider cloud storage (AWS S3, Google Cloud Storage)
6. **Rate Limiting**: Add rate limiting middleware
7. **Build Frontend**: Run `npm run build` in frontend directory
8. **Reverse Proxy**: Use Nginx or similar
9. **Process Manager**: Use PM2 or similar to keep backend running

## Support

For issues or questions:
- Check the main [README.md](README.md)
- Review API documentation in README
- Check GitHub issues

## License

This project is open source and available under the terms specified in the repository.
