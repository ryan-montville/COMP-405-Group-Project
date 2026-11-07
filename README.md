# COMP 405 Group Project

## Group Members

* Bazid Khan
* Isabella Alongi
* Jesus Gamez
* Ryan Montville

## Final Project Phase 1: Database Design & Modeling  

## Brief Explanation of Database  

The database serves a music streaming service application.  

The music streaming service database is designed to manage the streaming service and organization platform where users can listen, favorite, and organize their music in various forms.  

It will store and create relationships between information concerning the users, artists, playlists, albums, and songs. Moreover, according to the design and modeling, users can create multiple playlists, add songs to existing playlists, and favorite artists, bands, albums, and songs.

## ER Diagram: Shows Entities, Attributes, and Relationships

Note: [Here is a link](Note: Here is a link, ERD_draw.io, to view the ER Diagram in a closer view when opened with draw.io.), ERD_draw.io, to view the ER Diagram in a closer view when opened with draw.io.

## Design Decisions / Assumptions

* A user can own any number of playlists, but each playlist belongs to exactly one user Playlist (1,1) in OWNS
* A band must have at least one artist, but an artist does not have to belong to a band: Band (1, N) and Artist(0,N) in MEMBER_OF
* An album must contain at least one song, but a song does not have to be on an album, because singles exist. Album (1,N) and Song (0,N) in contains
* Playlists can be empty, and favorites are optional on both sides (partial part)
* A song or album can be released by either a solo artist or a band. To show this,  it was easier to make two separate releases relationships, one from Artist and one from Band.  Song and Album are (0,1) in each.

## Primary Keys, Foreign Keys, Constraints

Users(user_id, username, email, phone_number, dob, location)

* Primary Key: user_id

Artists(artist_id, artist_name, dob, years_active, genres, website)

* Primary Key: artist_id

Artist_Bands(artist_id, band_id)

* Primary Key: artist_id, band_id
* Foreign Keys:  
  * artist_id references Artists
  * band_id references Bands

User_Artists_Favorites(user_id, artist_id)

* Primary Key: user_id, artist_id
* Foreign Keys:
  * user_id references Users
  * artist_id references Artist

Bands(band_id, band_name, genres, years_active)

* Primary Key: band_id

User_Bands_Favorites(user_id, band_id)

* Primary Key: user_id, band_id
* Foreign Keys:
  * user_id references Users
  * band_id references Bands

Songs(song_id, song_title, length, release_date, artist_id, band_id)

* Primary Key: song_id
* Foreign Keys:
  * artist_id references Artists (nullable)
  * Band_id references Bands (nullable)
* Constraints:
  * Must have one foreign key (band_id or artist_id)

User_Song_Favorites(user_id, song_id)

* Primary Key: user_id, song_id
* Foreign Keys:
  *user_id references Users
  * song_id references Songs

Albums(album_id, album_title, release_date, artist_id,  band_id)

* Primary Key: album_id
* Foreign Keys:
  * artist_id (nullable)
  * Band_id (nullable)
* Constraints:
  *Must have one foreign key (artist_id or band_id)

Album_Song(album_id, song_id)

* Primary Key: album_id, song_id
* Foreign Keys:
  * album_id references Albums
  * song_id references Songs

User_Album_Favorites(user_id, album_id)

* Primary Key: user_id, album_id
* Foreign Keys:
  * user_id referenced Users
  * album_id references Albums

Playlists(playlist_id, playlist_name, user_id)

* Primary Key: playlist_id
* Foreign Key: user_id references Users

Song_Playlist(playlist_id, song_id)

* Primary Key: playlist_id, song_id
* Foreign Keys:
  * playlist_id references Playlists
  * song_id references Songs

## Relationships

* User can favorite many Artists, which can be favorited by many users (M:N)
* User can favorite many Songs, which can be favorited by many users (M:N)
* User can favorite many Albums, which can be favorited by many users (M:N)
* User can favorite many Bands, which can be favorited by many users (M:N)
* Users can have many Playlists, playlists belong to 1 User (1:N)
* Artists can belong to many Bands, Bands have many Artists (M:N)
* Artists can have many Songs/Albums, Bands can have many Songs/Albums. Each Song/Album is released by exactly one Artist OR one Band (1:N)
* Playlists have many Songs, Songs can be on many Playlists (M:N)
* Albums can have many Songs, Songs can be on many Albums (M:N)
