# -TCP-Socket-using-Python-
import socket

# Create a socket object
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print("Socket successfully created")

# Get local machine name
host = socket.gethostname()
port = 1234

# Bind to the port
server.bind((host, port))
print(f"Socket bound to {port}")

# Start listening for incoming connections
server.listen(1)
print("Socket is listening")

# Establish connection with client
client, addr = server.accept()
print(f"Got connection from {addr}")

while True:
    data = client.recv(1024)
    if not data:
        break
    print(f"Received {data.decode()} from the client")
    if data.decode() == 'Hello Server':
        client.send("Welcome".encode())
    elif data.decode() == 'disconnect':
        client.send("Goodbye".encode())
        break
    else:
        client.send("Invalid data".encode())

client.close()
