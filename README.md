# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
SERVER ALGORITHM:

1.Initialize the Server Socket Create a TCP socket using the socket library and define the server IP address (0.0.0.0) and port number (5001).

2.Bind and Listen Bind the socket to the specified IP address and port, then put the server into listening mode to wait for incoming client connections.

3.Accept Client Connection Accept an incoming connection request from a client and establish a communication link with the client.

4.Receive File Name Receive the name of the file from the client using the socket and prepare a new file on the server side with a prefix such as received_.

5.Receive and Store File Data Continuously receive the file data in fixed-size chunks and write the received data into the newly created file until the transmission ends.

6.Terminate Connection Close the file, client connection, and server socket after successful file reception.

CLIENT ALGORITHM:

1.Start the Program and Get File Name Prompt the user to enter the name of the file to be sent and verify whether the file exists in the local system.

2.Create Client Socket Create a TCP socket using the socket library for communication with the server.

3.Establish Connection with Server Connect the client socket to the server using the specified server IP address and port number.

4.Send File Name to Server Send the file name to the server so that the server can create a destination file.

5.Read and Send File Data Open the file in binary mode, read the file data in fixed-size chunks, and continuously send the data to the server until the end of the file is reached.

6.Close the Connection After successful transmission, close the client socket and terminate the program.

## PROGRAM
### server side
```
import socket
HOST="0.0.0.0"   
PORT=5001
BUFFER_SIZE=4096
server=socket.socket()
server.bind((HOST, PORT))
server.listen(1)
print("Server listening on port", PORT)
conn, addr=server.accept()
print("Connected from", addr)
filename=conn.recv(BUFFER_SIZE).decode()
print("Receiving file:", filename)
with open("received_" + filename, "wb") as file:
    while True:
        data=conn.recv(BUFFER_SIZE)
        if not data:
            break
        file.write(data)
print("File received successfully.")
conn.close()
server.close()
```
###client
```
import socket
import os
SERVER_IP="127.0.0.1" 
PORT=5001
BUFFER_SIZE=4096
filename=input("Enter file name to send: ")
if not os.path.exists(filename):
    print("File not found!")
    exit()
client=socket.socket()
client.connect((SERVER_IP, PORT))
client.send(filename.encode())
with open(filename, "rb") as file:
    while True:
        data=file.read(BUFFER_SIZE)
        if not data:
            break
        client.send(data)
print("File sent successfully.")
client.close()
```
## OUPUT
###client
<img width="837" height="469" alt="image" src="https://github.com/user-attachments/assets/c13a9aba-27d5-41c1-93d9-69f465d31212" />

###server 
<img width="839" height="469" alt="image" src="https://github.com/user-attachments/assets/91d496c0-7513-495d-b001-e21bb96c036a" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
