# COMP9331
Networking

# Instant_Messaging_Application

1. Project specification:

● Project: Instant messaging application 
● Language: Python 3.5.2 Imported 
● Module: socket, select, threading, time 
● Start server: python3 server.py port duration_time timeout 
● Stop server: KeyboardInterrupt (ctrl + c) 
● Start client: python3 client.py ip port 
● Stop server: logout or KeyboardInterrupt (ctrl + c)

2. Application layer protocol:

This instant messaging application includes 2 major modules, the server program and the client program.

This application is based on a chatting server which could handle requests from multi clients. Clients exchange data with this chatting server by TCP network protocol for communication. The protocol of this instant messaging application allows multiple clients connect at the same server and send messages through network.

3. Select module for I/O multiplexing:

This select module allows high-level and efficient I/O multiplexing. It is waiting for an input ( client socket or client data) when channel is ready.

select.select(rlist, wlist, xlist[, timeout])

This application used this select interface to wait for the rlist (wait it until ready for reading) which contain the connection request from the client or the data sending from the client. The timeout argument was used to call a function to logout inactive clients.

By the server main loop, connections are added for serving the requests of the client and removed from the rlist. This main loop selecting to block and wait for network activity. All of the sockets in the rlist which is readable list incoming data buffered and available to be process.

The rlist sockets represent three possible cases. If the socket is the main “server socket”, the one being used to listen for connections, then the readable condition means it is ready to accept another incoming connection. In addition to adding the new connection to the list of inputs to monitor, this section sets the client socket to not block. Next, an established connection with a client’s data sending to the server. The data is read from recv(), then placed on the queue so it can be analysed the first word (command) of the message and being processed by the server. 4. Client:

The major functions of this simple client application are:

● Creating socket to connect to the server

● Keeping connection with the serve

● Sending user’s input to server

● Receiving data from the server

● Sending logout request to server

5. Server:

This server of the instant messaging application is an all around application with every function listed in the specification. The server always runs first to wait for connection from clients and analyzes every data from the client. All messages between clients will be send via the server.

The major functions of this server are:

● User Authenticate: After client socket accepted by server socket, if login information (username , password) is valid, this chatting server system begin to process this client’s command and messages. Otherwise, the server socket will close the connection between server and client. After the server accepted connection requests from clients, the server will provide at most three times login authentication to the clients. Each client is distinguished from others by a unique username.

● Broadcast: This function is used for informing login/logout status for each client and forwarding broadcast messages from each sender.

● Online message: If the receiver is online, the server will find it’s socket and forward the message to this receiver.

● Offline message: If the receiver is offline, the server will keep offline messages and forward them to this user after he login.

● Whoelse: List all the online users except the command sender.

● Whoelsesince time: List all the online users since this time except the command sender.

● Blacklisting: User A can block the other user say B. B will not be informed A’s login or logout status report. B cannot send messages to A.

● Timeout: Eject a client from the server. During a specific time period, if User A does not send any data to the server, The server will log this user out. There are two ways to delivery Timeout function. Firstly, a timeout threading is opened for checking the inactivity user when there is no activity socket in the select module.In the imported select module, there is a fourth parameter which is used a Timeout. Secondly another Timeout function is also call to periodically check the inactivity users when there are activities in the server socket.

6. Reference :

● https://docs.python.org/3/library/select.html

● http://www.bogotobogo.com/python/python_network_programming_tcp_serve r_client_chat_server_chat_client_select.php
