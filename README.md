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

Server Code:

server.py

~~~
import socket

host = '127.0.0.1'
port = 8080

server = socket.socket()
server.bind((host, port))
server.listen(1)

print("Server running...")

while True:

    conn, addr = server.accept()

    print("Connected by:", addr)

    data = conn.recv(4096).decode()

    print("\nReceived Request:\n")
    print(data)

    response = """
HTTP/1.1 200 OK

<!DOCTYPE html>
<html>
<head>
<title>Simple Python Server</title>
</head>

<body>

<h1>Welcome to My Python Web Server</h1>

</body>
</html>
"""

    conn.send(response.encode())

    conn.close()
~~~

Client Code:

client.py

~~~
import socket


def send_request(host, port, request):

    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:

        s.connect((host, port))

        s.sendall(request.encode())

        response = s.recv(4096).decode(errors='ignore')

    return response


host = '127.0.0.1'
port = 8080

request = "GET / HTTP/1.1\r\nHost: localhost\r\n\r\n"

response = send_request(host, port, request)

print("Server Response:\n")

print(response)
~~~
## OUTPUT

<img width="1368" height="530" alt="image" src="https://github.com/user-attachments/assets/87baef22-055e-47be-9c62-2338bb075cd4" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
