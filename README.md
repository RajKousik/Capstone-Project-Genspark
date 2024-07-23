# Music App System

## 1. Requirements

### Functional Requirements

- User Registration and Authentication
- Song Listings
- Music Streaming
- Playlist Management
- Payment Integration (for premium users, Stripe if possible)
- Admin Management

## 2. System Architecture

### 2.1. Backend

- **ASP.NET Core**: For handling business logic and API endpoints.
- **Entity Framework Core**: For database operations and ORM.

### 2.2. Database

- **SQL Server**: For storing all the application data.

### 2.3. Authentication

- Use **ASP.NET Identity** for user authentication and authorization.

## 3. Database Design

### 3.1. Tables

- **Users**: UserId, Username, PasswordHash, Email, Role (Admin, Normal User, Premium User), CreatedAt
- **Songs**: SongId, Title, Artist, Album, Genre, Duration, ReleaseDate, Url
- **Playlists**: PlaylistId, UserId (references Users), Name, CreatedAt
- **PlaylistSongs**: PlaylistSongId, PlaylistId (references Playlists), SongId (references Songs)
- **Artists**: ArtistId, Name, Bio, ImageUrl
- **Albums**: AlbumId, Title, ArtistId (references Artists), ReleaseDate, Genre, CoverImageUrl
- **Genres**: GenreId, Name, Description
- **Favorites**: FavoriteId, UserId (references Users), SongId (references Songs, nullable if favorites a playlist), PlaylistId (references Playlists, nullable if favorites a song)

## 4. API Design

### 4.1. User APIs

- **POST** /api/users/register: Register a new user.
- **POST** /api/users/login: Authenticate a user.
- **GET** /api/users/profile: Get user profile.
- **PUT** /api/users/profile: Update user profile.
- **GET** /api/users/favorites: Get user favorites.

### 4.2. Song APIs

- **GET** /api/songs: Get a list of songs.
- **GET** /api/songs/{id}: Get details of a specific song.

### 4.3. Playlist APIs

- **POST** /api/playlists: Create a new playlist.
- **GET** /api/playlists: Get a list of playlists for a user.
- **GET** /api/playlists/{id}: Get details of a specific playlist.
- **PUT** /api/playlists/{id}: Update a playlist.
- **DELETE** /api/playlists/{id}: Delete a playlist.

### 4.4. PlaylistSongs APIs

- **GET** /api/playlists/{id}/songs: Get all songs in a playlist.
- **POST** /api/playlists/{id}/songs: Add a song to a playlist.
- **DELETE** /api/playlists/{id}/songs/{songId}: Remove a song from a playlist.
- **GET** /api/playlists/{id}/songs/{songId}: Get details of a specific song in a playlist.

### 4.5. Artist APIs

- **GET** /api/artists: Get a list of artists.
- **GET** /api/artists/{id}: Get details of a specific artist.

### 4.6. Album APIs

- **GET** /api/albums: Get a list of albums.
- **GET** /api/albums/{id}: Get details of a specific album.

### 4.7. Genre APIs

- **GET** /api/genres: Get a list of genres.
- **GET** /api/genres/{id}: Get details of a specific genre.

### 4.8. Favorites APIs

- **GET** /api/favorites: Get a list of user favorites.
- **POST** /api/favorites/songs: Add a song to favorites.
- **DELETE** /api/favorites/songs/{songId}: Remove a song from favorites.
- **POST** /api/favorites/playlists: Add a playlist to favorites.
- **DELETE** /api/favorites/playlists/{playlistId}: Remove a playlist from favorites.

## 5. Endpoints

### Admin Endpoints

Admin endpoints are used by administrators to manage the system. These endpoints often include CRUD (Create, Read, Update, Delete) operations for songs, artists, albums, genres, and user management.

#### User Management

- **GET** /api/admin/users: Get a list of all users.
- **GET** /api/admin/users/{id}: Get details of a specific user.
- **DELETE** /api/admin/users/{id}: Delete a user.

#### Song Management

- **POST** /api/admin/songs: Add a new song.
- **PUT** /api/admin/songs/{id}: Update song details.
- **DELETE** /api/admin/songs/{id}: Delete a song.
- **GET** /api/admin/songs: Get a list of all songs (with detailed administrative info).

#### Playlist Management

- **GET** /api/admin/playlists: Get a list of all playlists.
- **GET** /api/admin/playlists/{id}: Get details of a specific playlist.
- **DELETE** /api/admin/playlists/{id}: Delete a playlist.

#### Artist Management

- **POST** /api/admin/artists: Add a new artist.
- **PUT** /api/admin/artists/{id}: Update artist details.
- **DELETE** /api/admin/artists/{id}: Delete an artist.
- **GET** /api/admin/artists: Get a list of all artists.

#### Album Management

- **POST** /api/admin/albums: Add a new album.
- **PUT** /api/admin/albums/{id}: Update album details.
- **DELETE** /api/admin/albums/{id}: Delete an album.
- **GET** /api/admin/albums: Get a list of all albums.

#### Genre Management

- **POST** /api/admin/genres: Add a new genre.
- **PUT** /api/admin/genres/{id}: Update genre details.
- **DELETE** /api/admin/genres/{id}: Delete a genre.
- **GET** /api/admin/genres: Get a list of all genres.
