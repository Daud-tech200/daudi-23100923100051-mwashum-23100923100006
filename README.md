# TCP Socket Chat — Python

A simple TCP client-server communication example built with Python's `socket` module.

## Files

| File | Description |
|------|-------------|
| `server.py` | Starts a TCP server, waits for a client connection, and echoes received messages back |
| `client.py` | Connects to the server and sends messages |

> **Note:** Both files currently contain identical server-side code. `client.py` likely needs to be updated with actual client logic (see [Usage](#usage) below for what it should look like).

## Requirements

- Python 3.x (no external dependencies)

## Usage

### 1. Start the server

```bash
python server.py
```

The server binds to `0.0.0.0:5000` and waits for an incoming connection.

### 2. Connect with a client

In a separate terminal, run (or write) the client:

```bash
python client.py
```

A basic client implementation to pair with this server:

```python
import socket

HOST = "127.0.0.1"
PORT = 5000

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((HOST, PORT))

while True:
    message = input("You: ")
    client.send(message.encode())

    response = client.recv(1024).decode()
    print("Server:", response)

client.close()
```

## How It Works

1. The server creates a TCP socket and listens on port `5000`.
2. When a client connects, the server enters a receive loop.
3. Each message received is printed and echoed back as `"Server received: <message>"`.
4. The loop ends when the client disconnects (empty data received).

## Configuration

Both `HOST` and `PORT` are defined at the top of each file:

```python
HOST = "0.0.0.0"  # Change to "127.0.0.1" to restrict to localhost
PORT = 5000       # Change to any available port
```

## Notes

- Only one client connection is handled at a time. For multiple concurrent clients, consider using `threading` or `asyncio`.
- There is no authentication or encryption. Do not expose this server to untrusted networks as-is.
