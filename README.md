# Group Chat Application

## TCP Design
### Server
We set up a server to handle the mutiple requests using **Thread**. At the moment, we have a fixed number of threads equals to 10. Each client has his/her own thread so our server can only handle maximum 10 clients. We will look for better solution in our freetime since our UDP chat app is our main focus at the moment.

Back to our design priciples, when a request comes, a server get connection and address. We save the connection object and IP from the address in a dictionary as the format `{ConnectionObject : IP}`.  We get the data from the connection object and send back to all the client in that dictionary.

### Client
Each client have 2 threads: one to send and one to receive.

## UDP Design
### Server:
We set up the server that listen to all the connections. Whenever a request comes, a server first get the data and address. Since in the client side, we set the first message sent by the client is his/her username. We use that data to store the username in a dictionary as the format: `{IP : [username, address_port, message_count]}`

Each time the **same** client login, he/she has the same IP but different port. We save the address port so we can update it constantly. The message count is used to count the message received of each client. It increases by 1 everytime the client send a new message. In the future, we can use that sequential proof to prevent data loss.

Now we have the username from the first message, so from the second message, we only received data from the client. We save that data in an array which holds the username and data. We know username of the sender, so we don't have to use the IP as an indentifier.

In the end, we use the client's dictionary to notify everyone in the group chat.

### Client
Each client have 2 threads: one to send and one to receive.

## Testing
For both TCP and UDP:
- Make sure all the machine you are testing are on the **same network**.
- Run the server file on **1 machine** and client file on **diffrent machines**.
- Follow the client file instruction.

## Errors
### TCP
- **OSError: [Errno 9] Bad file descriptor:** It happens when a client uses ^C to quit the chat.
- ~~**[errno 48] address already in use:** It happens because we don't close the socket properly.~~

## To-do
### Both
- ~~Write a desgin doc~~
- Error Handling

### TCP
- ~~Fix oserror: per permanently~~
- Open a new thread whenever a new connection ask for, custom thread number?, limit?
- Client have a custom username
- Nidesh DDoS acttack idea, "Around the World" one.

### UDP
- ~~UDP multicast~~
- ~~Login screen~~
- ~~Send a number with a message to keep the count and make sure all messages are delivered~~
- Error handling
- Curses module for seperate chat screen
- Special escape
- Add doc's requirements

## Questions/ Write-up
- How to do without threading? Message queue?

