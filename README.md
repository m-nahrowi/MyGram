# MyGram Project

MyGram adalah sebuah aplikasi yang memungkinkan pengguna untuk menyimpan dan berbagi foto serta membuat komentar pada foto orang lain. Proyek ini dilengkapi dengan proses CRUD (Create, Read, Update, Delete) menggunakan tabel dan alur yang dijelaskan di bawah ini:

## Framework dan Library

Project ini direkomendasikan menggunakan framework Gin Gonic dan ORM Gorm. Library/package wajib yang digunakan:

- [github.com/dgrijalva/jwt-go](https://github.com/dgrijalva/jwt-go)
- [golang.org/x/crypto](https://pkg.go.dev/golang.org/x/crypto)

## Struktur Database

### User

- id (Primary key)
- username (string)
- email (string)
- password (string)
- age (integer)
- created_at (Date)
- updated_at (Date)

### Photo

- id (Primary key)
- title (string)
- caption (string)
- photo_url (string)
- user_id (Foreign Key dari Tabel User)
- created_at (Date)
- updated_at (Date)

### Comment

- id (Primary Key)
- user_id (Foreign Key dari Tabel User)
- photo_id (Foreign Key dari Tabel Photo)
- message (string)
- created_at (Date)
- updated_at (Date)

### SocialMedia

- id (Primary Key)
- name (String/ varchar)
- social_media_url (String/ Text)
- UserId (Foreign Key dari Tabel User)
- created_at (Date)
- updated_at (Date)

## Validasi

Validasi untuk tiap-tiap field pada tabel:

### User

1. **email**
   - Format email yang valid
   - Unique index
   - Tidak boleh kosong
2. **username**
   - Unique index
   - Tidak boleh kosong
3. **password**
   - Minimal 6 karakter
   - Tidak boleh kosong
4. **age**
   - Minimal 8
   - Tidak boleh kosong

### Photo

1. **title**
   - Tidak boleh kosong
2. **photo_url**
   - Tidak boleh kosong

### SocialMedia

1. **name**
   - Tidak boleh kosong
2. **social_media_url**
   - Tidak boleh kosong

### Comment

1. **message**
   - Tidak boleh kosong

## Alur Aplikasi

- Untuk mengakses data pada tabel SocialMedia, Photo, dan Comment, pengguna harus melewati proses autentikasi menggunakan JsonWebToken.
- Modifikasi data kepemilikan seperti update atau delete harus melewati proses autorisasi.

## Endpoint

### Users

- **POST /users/register**
  - Request Body:
    ```
    {
      // Data user
    }
    ```
  - Response: 
    ```
    {
      // Data user
    }
    ```

- **POST /users/login**
  - Request Body:
    ```
    {
      // Email dan password user
    }
    ```
  - Response:
    ```
    {
      // Data user dan token
    }
    ```

- **PUT /users**
  - Request Headers: Authorization (Bearer token string)
  - Request Params: userId (integer)
  - Request Body:
    ```
    {
      // Data user yang ingin diupdate
    }
    ```
  - Response:
    ```
    {
      // Data user yang sudah diupdate
    }
    ```

- **DELETE /users**
  - Request Headers: Authorization (Bearer token string)
  - Response:
    ```
    {
      // Pesan konfirmasi
    }
    ```

### Photos

- **POST /photos**
  - Request Headers: Authorization (Bearer token string)
  - Request Body:
    ```
    {
      // Data photo
    }
    ```
  - Response:
    ```
    {
      // Data photo yang berhasil disimpan
    }
    ```

- **GET /photos**
  - Request Headers: Authorization (Bearer token string)
  - Response:
    ```
    {
      // Data photo
    }
    ```

- **PUT /photos/:photoId**
  - Request Headers: Authorization (Bearer token string)
  - Request Params: photoId (string)
  - Request Body:
    ```
    {
      // Data photo yang ingin diupdate
    }
    ```
  - Response:
    ```
    {
      // Data photo yang sudah diupdate
    }
    ```

- **DELETE /photos/:photoId**
  - Request Headers: Authorization (Bearer token string)
  - Request Params: photoId (integer)
  - Response:
    ```
    {
      // Pesan konfirmasi
    }
    ```

### Comments

- **POST /comments**
  - Request Headers: Authorization (Bearer token string)
  - Request Body:
    ```
    {
      // Data comment
    }
    ```
  - Response:
    ```
    {
      // Data comment yang berhasil disimpan
    }
    ```

- **GET /comments**
  - Request Headers: Authorization (Bearer token string)
  - Response:
    ```
    {
      // Data comment
    }
    ```

- **PUT /comments/:commentId**
  - Request Headers: Authorization (Bearer token string)
  - Request Params: commentId (integer)
  - Request Body:
    ```
    {
      // Data comment yang ingin diupdate
    }
    ```
  - Response:
    ```
    {
      // Data comment yang sudah diupdate
    }
    ```

- **DELETE /comments/:commentId**
  - Request Headers: Authorization (Bearer token string)
  - Request Params: commentId (integer)
  - Response:
    ```
    {
      // Pesan konfirmasi
    }
    ```

### SocialMedias

- **POST /socialmedias**
  - Request Headers: Authorization (Bearer token string)
  - Request Body:
    ```
    {
      // Data social media
    }
    ```
  - Response:
    ```
    {
      // Data social media yang berhasil disimpan
    }
    ```

- **GET /socialmedias**
  - Request Headers: Authorization (Bearer token string)
  - Response:
    ```
    {
      // Data social media
    }
    ```

- **PUT /socialmedias/:socialMediaId**
  - Request Headers: Authorization (Bearer token string)
  - Request Params: socialMediaId (integer)
  - Request Body:
    ```
    {
      // Data social media yang ingin diupdate
    }
    ```
  - Response:
    ```
    {
      // Data social media yang sudah diupdate
    }
    ```

- **DELETE /socialmedias/:socialMediaId**
  - Request Headers: Authorization (Bearer token string)
  - Request Params: socialMediaId (integer)
  - Response:
    ```
    {
      // Pesan konfirmasi
    }
    ```
## Catatan

- Pastikan seluruh routing endpoint diikuti dengan betul.
- Request body, headers, maupun request params harus diikuti dengan betul.
- Response status dan response data harus diikuti dengan betul.
- Perhatikan catatan yang telah diberikan, seperti endpoint-endpoint yang harus melewati proses autentikasi dan autorisasi.
- Proses autorisasi dilakukan setelah proses autentikasi, bukan sebaliknya.
