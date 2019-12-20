# decrypt
This is a repository for decryption using OpenSSL

## Usage

1. Generate the private key using RSA
   ```
   openssl genrsa -aes256 -out private2.pem 2048
   ```
2. Generate the public key using RSA
   ```
   openssl rsa -in private2.pem -pubout > public2.pem
   ```
3. Decrypt the session key using the private key
   ```
   openssl rsautl -decrypt -inkey private2.pem -in session.enc -out session.txt
   cat session.txt
   ```
4. Decrypt the message using 256-bit AES in CBC mode
   ```
   openssl enc -d -aes-256-cbc -salt -in message.enc -out message.txt
   ```
5. Decrypt the session key using 256-bit AES in CBC mode with session key
   ```
   openssl enc -d -aes-256-cbc -salt -in signature.enc -out signature.txt
   ```
6. Compare the expected signiture with the original signiture
   ```
   openssl dgst -sha256 -verify public.pem -signature signature.txt message.txt
   ```