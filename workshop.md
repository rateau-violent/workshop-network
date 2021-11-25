## step 1
Créer un serveur qui listen sur le port 8080 et qui print "New client connected" quand un client se connecte.
Le serveur doit print tout les messages que le client lui envoie.

Créer un client qui va se connecter à localhost:8080 et qui va envoyer hello world, toutes les 1 secondes.

ref (server):
```python
import socket

BUFF_SIZE = 8192
ADDRESS = ("127.0.0.1", 8080)

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as server:
    server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server.bind(ADDRESS)
    server.listen()

    connection, client = server.accept()
    while True:
        data = connection.recv(BUFF_SIZE)
        print(data)
```

ref (client):
```python
import socket
import time

HOST = "127.0.0.1"
PORT = 8080

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as sock:
    sock.connect((HOST, PORT))

    while True:
        sock.send(b'Hello, world')
        time.sleep(1)
```
____

Step 2
Créer un serveur qui gère plusieurs clients et qui les identifie en fonction de leur ordre de connection
(la difficulté c'est que recv est bloquant, donc faut utiliser select)

ref (serveur:)
```python
import select
import socket

BUFF_SIZE = 8192


class Server:
    def __init__(self, port: int):
        self._socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        self._socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        self._socket.bind(("127.0.0.1", port))
        self._socket.listen()
        self._clients = []
        self._running = False

    def run(self):
        self._running = True

        while self._running:
            read_set = [self._socket] + self._clients
            read_ready, write_ready, exceptions = select.select(read_set, [], read_set)
            for current in read_ready:
                if current == self._socket:
                    self._accept_client()
                else:
                    data = current.recv(BUFF_SIZE)
                    print("client {}> {}".format(self._clients.index(current), data))

    def _accept_client(self):
        client, client_address = self._socket.accept()
        self._clients.insert(len(self._clients), client)


s = Server(8080)

s.run()
```
___
Step 3:

Créer un serveur qui supporte trois commandes: `/login`, `/message`, `/text`.
`/login (nickname)`
`/message (destination) (message)`
`/text (destination) (message)`

descriptions:
`/login` permet de choisir son username sur le serveur.
`/message` permet d'envoyer un message à un username
`/text` permet d'envoyer un message à tout les utilisateurs

formats:
`/message`: Private message from {SENDER_USERNAME}: {MESSAGE_CONTENT}
`/text`: {SENDER_USERNAME}: {MESSAGE_CONTENT}

ref (server):
```python

```