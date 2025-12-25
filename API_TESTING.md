# API Testing Examples

This file contains example API requests you can use to test the EchoBolt backend.

## Authentication

### Register a New User

```bash
curl -X POST http://localhost:1337/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "username": "testuser",
    "email": "test@example.com",
    "password": "password123"
  }'
```

**Response:**
```json
{
  "message": "User registered successfully",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "...",
    "username": "testuser",
    "email": "test@example.com"
  }
}
```

### Login

```bash
curl -X POST http://localhost:1337/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "password123"
  }'
```

**Save the token from the response for authenticated requests!**

---

## Songs

### Get All Songs

```bash
curl http://localhost:1337/api/v1/songs
```

### Upload a Song (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"

curl -X POST http://localhost:1337/api/v1/songs/upload \
  -H "Authorization: Bearer $TOKEN" \
  -F "title=My Favorite Song" \
  -F "artist=Amazing Artist" \
  -F "audio=@/path/to/your/song.mp3"
```

### Stream a Song

```bash
# Get the filename from the songs list first
curl http://localhost:1337/api/v1/songs/stream/1234567890-song.mp3 --output song.mp3
```

### Delete a Song (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"
SONG_ID="song_id_here"

curl -X DELETE http://localhost:1337/api/v1/songs/$SONG_ID \
  -H "Authorization: Bearer $TOKEN"
```

---

## Playlists

### Create a Playlist (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"

curl -X POST http://localhost:1337/api/v1/playlist/create \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "My Favorites",
    "description": "Songs I love"
  }'
```

### Get All Playlists (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"

curl http://localhost:1337/api/v1/playlist/ \
  -H "Authorization: Bearer $TOKEN"
```

### Get a Specific Playlist (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"
PLAYLIST_ID="playlist_id_here"

curl http://localhost:1337/api/v1/playlist/$PLAYLIST_ID \
  -H "Authorization: Bearer $TOKEN"
```

### Add Song to Playlist (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"
PLAYLIST_ID="playlist_id_here"
SONG_ID="song_id_here"

curl -X POST http://localhost:1337/api/v1/playlist/add/$PLAYLIST_ID \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "songId": "'$SONG_ID'"
  }'
```

### Remove Song from Playlist (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"
PLAYLIST_ID="playlist_id_here"
SONG_ID="song_id_here"

curl -X DELETE http://localhost:1337/api/v1/playlist/remove/$PLAYLIST_ID \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "songId": "'$SONG_ID'"
  }'
```

### Delete a Playlist (Requires Authentication)

```bash
TOKEN="your_jwt_token_here"
PLAYLIST_ID="playlist_id_here"

curl -X DELETE http://localhost:1337/api/v1/playlist/$PLAYLIST_ID \
  -H "Authorization: Bearer $TOKEN"
```

---

## Testing with Postman

1. Import these requests into Postman
2. Create an environment variable `TOKEN` for authentication
3. After login/register, copy the token to the environment variable
4. Use `{{TOKEN}}` in the Authorization header

---

## Testing Workflow Example

```bash
# 1. Register
curl -X POST http://localhost:1337/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"username":"demo","email":"demo@example.com","password":"demo123"}'

# Copy the token from response
TOKEN="paste_token_here"

# 2. Upload a song
curl -X POST http://localhost:1337/api/v1/songs/upload \
  -H "Authorization: Bearer $TOKEN" \
  -F "title=Test Song" \
  -F "artist=Test Artist" \
  -F "audio=@song.mp3"

# 3. Get all songs
curl http://localhost:1337/api/v1/songs

# 4. Create a playlist
curl -X POST http://localhost:1337/api/v1/playlist/create \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name":"Favorites","description":"My favorite songs"}'

# 5. Add song to playlist (use IDs from previous responses)
curl -X POST http://localhost:1337/api/v1/playlist/add/PLAYLIST_ID \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"songId":"SONG_ID"}'
```

---

## Health Check

Test if the API is running:

```bash
curl http://localhost:1337
```

Expected response:
```json
{
  "message": "EchoBolt API is running"
}
```
