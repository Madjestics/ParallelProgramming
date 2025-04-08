## В рамках задачи выполнялось ознакомление и работа с Java IPC. Созданы клиент и сервер, которые обмениваются между собой сообщениями через socket.

### Результат работы программы сервера:
Server is running and waiting for connections...\
New client connected: Socket[addr=/127.0.0.1,port=54131,localport=12346]\
User Dima connected.\
New client connected: Socket[addr=/127.0.0.1,port=54135,localport=12346]\
User User connected.\
Hello everyone\
[Dima]: Hi\
[User]: Hi

### Результат работы программы клиента-1:
Connected to the chat server!\
Enter your username:\
Dima\
Welcome to the chat, Dima!\
Type Your Message\
[Server]: Hello everyone\
Hi\
[User]: Hi

### Результат работы программы клиента-2:
Connected to the chat server!\
Enter your username:\
User\
Welcome to the chat, User!\
Type Your Message\
[Server]: Hello everyone\
[Dima]: Hi\
Hi

##### Как видно из результатов, процессы-клиенты и сервер взаимодействуют корректно, выводя сообщения.
