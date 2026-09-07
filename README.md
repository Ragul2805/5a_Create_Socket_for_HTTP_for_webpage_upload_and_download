# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm

1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
**server**
```
import socket
import os

HOST = 'localhost'
PORT = 8000

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((HOST, PORT))
server.listen(5)

print("HTTP Server started...")
print("Open http://localhost:8000 in your browser")

while True:
    conn, addr = server.accept()

    request = conn.recv(1024).decode()

    print("\nClient Request:")
    print(request)

    if request.startswith("GET"):
        filename = "index.html"

        if os.path.exists(filename):
            with open(filename, "rb") as f:
                content = f.read()

            response = (
                b"HTTP/1.1 200 OK\r\n"
                b"Content-Type: text/html\r\n"
                b"Content-Length: " + str(len(content)).encode() +
                b"\r\n\r\n" + content
            )

            conn.sendall(response)
            print("Webpage sent successfully")

        else:
            response = (
                b"HTTP/1.1 404 Not Found\r\n"
                b"Content-Type: text/html\r\n\r\n"
                b"<h1>404 - File Not Found</h1>"
            )

            conn.sendall(response)

    conn.close()
```
**html**
```
<!DOCTYPE html>
<html>
<head>
    <title>Computer Networks</title>
</head>

<body>

    <h1>Welcome to My HTTP Server</h1>

    <p>This webpage is transferred using Python socket programming.</p>

    <h2>HTTP Webpage Upload and Download</h2>

    <p>Computer Networks Laboratory</p>

</body>
</html>
```
## OUTPUT
<img width="1912" height="852" alt="image" src="https://github.com/user-attachments/assets/f2404590-6977-417a-978b-4f90700eee8d" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
