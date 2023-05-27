
En una estructura cliente-servidor, para el caso de uso de registrarse, nos encontramos con el típico problema de que hashear las cosas client side no es seguro y acaba con los recursos de la máquina cliente (en especial si es en móvil), pero enviar la contraseña en plaintext, aunque sea en una conexión encriptada HTTPS, sigue sin ser seguro.

¿QUÉ HACEMOS?

ChatGPT propone lo siguiente:

Here's a high-level overview of a secure sign-up process that addresses the transmission concern:

1.  Client-Side: The Next.js client application can use a secure communication protocol, such as HTTPS, to establish an encrypted connection between the client and the server.
    
2.  Secure Key Exchange: Utilize secure key exchange protocols like Diffie-Hellman key exchange or the use of asymmetric encryption algorithms (e.g., RSA) to securely exchange encryption keys between the client and server.
    
3.  Encrypted Password Transmission: With a secure connection and established encryption keys, the client application can encrypt the password using the server's public key or a shared secret key before transmitting it to the server.
    
4.  Server-Side Decryption: The server, upon receiving the encrypted password, can then decrypt it using the corresponding private key (in the case of asymmetric encryption) or the shared secret key.
    

By incorporating encryption and secure key exchange protocols, you can protect the transmission of the password while still performing the password hashing and storage securely on the server-side. This approach mitigates the risk of transmitting plaintext passwords over an encrypted connection.

El algoritmo actualmente (25/05/2023) recomendado para hashear password es el Argon2, su variante Argon2Id siendo la más polivalente para ataques de uso intensivo de GPU o CPU.


