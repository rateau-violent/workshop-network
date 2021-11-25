# **[Workshop COBRA] - Network programming**

## **Step 1 - Basic server**

Create a python server that listens on port `8080` and prints "`New client connected !`" when a new client connects.

The server must also print every message sent by the clients.

*__Tips:__ You can test your server with already implemented clients like `nc` (man nc).*

---

## **Step 2 - Client**

Create a python client that connects to the server (localhost:8080) and sends a "`Hello world !`" message each second.

---

## **Step 3 - Multi-clients management**

Modify the server so it can manage multiple clients and identify them deoending on the connection order.

***__Tips__:** look `select`*

---

## **Step 4 - Server commands**

Add 4 commands to the server:
  - `/login [username]`: enables the users to chose their username on the server
  - `/message [receiver username] [message]`: enables the users to send a message to another one
  - `/text`: enables to send a message to all users
  - `/logout`: diconnects the user

All the commands arguments (like [username]) must be between double quotes.

The receiver must receive messages as follow:
- `/message`: Private message from {SENDER_USERNAME}: {MESSAGE_CONTENT}
- `/text`: [sender_username]: [message_content]
