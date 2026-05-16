# Project: Build a TCP Chat Server

## Overview
Learn Socket Programming by building a simple TCP Chat Server and Client using Python.

## Server Code (`server.py`)
```python
import socket
import threading

def handle_client(conn, addr):
    print(f"[NEW CONNECTION] {addr} connected.")
    connected = True
    while connected:
        msg = conn.recv(1024).decode('utf-8')
        if msg == "DISCONNECT":
            connected = False
        print(f"[{addr}] {msg}")
        conn.send("Msg received".encode('utf-8'))
    conn.close()

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('127.0.0.1', 9999))
server.listen()
print("[STARTING] Server is listening...")

while True:
    conn, addr = server.accept()
    thread = threading.Thread(target=handle_client, args=(conn, addr))
    thread.start()
```

## Client Code (`client.py`)
```python
import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect(('127.0.0.1', 9999))

client.send("Hello World!".encode('utf-8'))
print(client.recv(1024).decode('utf-8'))
client.send("DISCONNECT".encode('utf-8'))
```

## To Run
1. Run `python server.py` in one terminal.
2. Run `python client.py` in another terminal.
