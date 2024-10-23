# Authentication &. Authorization

In simple terms, authentication is the process of verifying who a user is, while authorization is the process of verifying what they have access to.

Comparing these processes to a real-world example, when you go through security in an airport, you show your ID to authenticate your identity. Then, when you arrive at the gate, you present your boarding pass to the flight attendant, so they can authorize you to board your flight and allow access to the plane.

![image](https://github.com/user-attachments/assets/bee0db51-1387-43c1-9c69-2049c7304c55)

# Ways Of Authentication

## Cookie Based Authentication

Since the HTTP protocol is stateless, this means that if we authenticate a user with a username and password, then on the next request, our application won’t know this is the same person from the previous request. We would have to authenticate again. At each request, HTTP doesn’t know anything about what happened before, it just carries the request. So for any request for private data, you would have to log in again to make sure the application knows this is really you. This would be very annoying.

To avoid this problem, session/cookie based authentication was introduced. It makes the authentication process **stateful**, This means that an authentication record or session must be kept both server and client-side. The server needs to keep track of active sessions in a database or memory, while on the front-end a cookie is created that holds a session identifier, thus the name cookie based authentication. This one is the most common and widely known method of authentication which is being used for a long time.

**Basic flow of cookie based authentication**:

- In the browser User enters his username and password and the request goes from the client application to the server.
Server checks for the user, authenticates it and sends a unique token to the user’s client application. (also saves this unique token in memory or database)

- The client application stores the token in cookies, and sends it back with each subsequent request.

- The server receives every request that requires authentication and uses the token to authenticate the user and return the requested data back to the client application.

- When someone logs out, the client application removes that token, and so that subsequent request to rails from the client becomes unauthorized.

![image](https://github.com/user-attachments/assets/fca76d1b-11dc-4a3d-abb9-1e222924ad03)

## Token based authentication:

Token-based authentication has gained prevalence over the last few years due to rise of single page applications, web APIs, and the Internet of Things (IoT). Token used for ‘Token based authentication’ is mostly Json Web Tokens(JWT). Though there are different implementations of tokens but the JWT have become the de-facto standard.

Token based authentication is stateless. We will not store any information about our user on the server or in a session, not even which JWTs have been issued to the clients.

**Basic flow of token based authentication**:

- User enters their login credentials

- Server verifies the credentials are correct and returns a signed token (the JWT) which can contain some additional information as a metadata like user_id, permissions etc.

- This token is stored client-side, most commonly in local storage — but can be stored in session storage or a cookie as well

- Subsequent requests to the server include this token generally as an additional Authorization header in form of Bearer {JWT}, but can additionally be sent in the body of a POST request or even as a query parameter.

- The server decodes the JWT and if the token is valid, processes the request

- Once a user logs out, the token is destroyed client-side, no interaction with the server is necessary

![image](https://github.com/user-attachments/assets/eb6f26bc-0226-440a-8d2b-c84fbd10bcba)

## Social Sign In

![image](https://github.com/user-attachments/assets/8c3bde0e-6329-4f08-be61-03b61f148fcf)

First of all, for the users, the login to your application is just one click away as they can use their existing social network account and don’t need to remember username, password for services like your application. This results in a rich user experience. Also as a developer you don’t need to worry about securing user’s authentication credentials and also you are ensured that user’s email address is already verified (by the social service providers). Another bonus point, social provider will also handle the password recovery process. Yay!

## Two-factor authentication 2FA

Relies on the concept of a user knowing and owning multiple credentials to access the application.

When withdrawing money, we use the bank card and the pin, knowing one of them is not enough to withdraw the money.

- Something you Know — the password or pin for an account
- Something you Have — a physical device such as a mobile phone or a software application that can generate one-time passwords
- Something you Are — a biologically unique feature to you such as your fingerprints, voice or retinas

![image](https://github.com/user-attachments/assets/e8fdcf95-8ad4-46e8-a5ef-584696edfa02)
