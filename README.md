JWKS Server Project 3 Documentation
This project is a secure JWKS (JSON Web Key Set) server that manages RSA key pairs and user authentication.
Project Overview
•	Encrypt and store RSA private keys using AES encryption.
•	User registration using the /register endpoint.
•	User login and JWT token issuance via the /auth endpoint.
•	Authentication logging with IP address and timestamps.
•	Rate limiting set at 5 authentication attempts per minute.
•	Public keys available at the /.well-known/jwks.json endpoint.
________________________________________
API Endpoints
1. Register User
Endpoint: POST /register
Input JSON:
{
  "username": "yourusername",
  "email": "youremail@example.com"
}
Response JSON:
{
  "password": "generated-uuid-password"
}
2. Authenticate User
Endpoint: POST /auth
Input JSON:
{
  "username": "yourusername",
  "password": "yourpassword"
}
Response JSON:
{
  "token": "signed-jwt-token"
}
•	If too many requests are made, a 429 Too Many Requests error is returned.
3. Get Public Keys
Endpoint: GET /.well-known/jwks.json
Returns public keys in JWKS format.
________________________________________
Database Structure
•	keys table: Stores encrypted private keys with expiration timestamps.
•	users table: Stores users with hashed passwords.
•	auth_logs table: Stores authentication attempts with IP and timestamps.
________________________________________
Technologies Used
•	Flask (API framework)
•	SQLite (Database)
•	Cryptography (AES encryption)
•	Argon2-cffi (Password hashing)
•	PyJWT (JWT generation)
•	Flask-Limiter (Rate limiting)
________________________________________
Setup Instructions
1.	Install required packages:
pip install flask flask-limiter cryptography pyjwt argon2-cffi
2.	(Optional) Set your own AES key:
export NOT_MY_KEY="your-32-byte-secret-key"
Otherwise, a default key will be used.
3.	Run the server:
python app.py
Server will start at: http://localhost:8080
________________________________________
Key Notes
•	Register users first using /register.
•	Authentication returns JWTs signed with a valid private key.
•	If no valid keys exist, /auth returns 404.
•	AES encryption uses PKCS7 padding.
•	Global rate limit is 5 /auth requests per minute.
________________________________________
Author
Created for CSCE 3550 - Project 3 Assignment.


