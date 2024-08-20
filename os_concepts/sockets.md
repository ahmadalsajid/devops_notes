[Home](../README.md)

### Sockets
**What is Socket?**  
Socket is a mechanism which provides connection between two process or system by using network stacks. In a more clear 
way we can use sockets communicate and transfer data between two system. As we know Unix and Linux systems works on 
file logic. Everything in operating system is file where network connections are files too.

**Use Cases**  
Sockets can be used in different cases.
* We can use socket to transfer data between two different process in same system.
* Send command to the remote system
* Download data from remote system

**Socket Types**  
There are four types of sockets available to the users. The first two are most commonly used and the last two are 
rarely used.Processes are presumed to communicate only between sockets of the same type but there is no restriction
that prevents communication between sockets of different types.  
* **Stream Sockets**: Delivery in a networked environment is guaranteed. If you send through the stream socket three 
  items "A, B, C", they will arrive in the same order − "A, B, C". These sockets use TCP (Transmission Control Protocol) 
  for data transmission. If delivery is impossible, the sender receives an error indicator. Data records do not have any 
  boundaries.
* **Datagram Sockets**: Delivery in a networked environment is not guaranteed. They're connectionless because you don't 
  need to have an open connection as in Stream Sockets − you build a packet with the destination information and send 
  it out. They use UDP (User Datagram Protocol).
* **Raw Sockets**: These provide users access to the underlying communication protocols, which support socket 
  abstractions. These sockets are normally datagram oriented, though their exact characteristics are dependent 
  on the interface provided by the protocol. Raw sockets are not intended for the general user; they have been 
  provided mainly for those interested in developing new communication protocols, or for gaining access to some 
  of the more cryptic facilities of an existing protocol.
* **Sequenced Packet Sockets**: They are similar to a stream socket, with the exception that record boundaries are 
  preserved. This interface is provided only as a part of the Network Systems (NS) socket abstraction, and is very 
  important in most serious NS applications. Sequenced-packet sockets allow the user to manipulate the Sequence 
  Packet Protocol (SPP) or Internet Datagram Protocol (IDP) headers on a packet or a group of packets, either by 
  writing a prototype header along with whatever data is to be sent, or by specifying a default header to be used 
  with all outgoing data, and allows the user to receive the headers on incoming packets.
  
References:
* [poftut](https://www.poftut.com/what-is-linux-unix-socket/)
* [tutorialspoint](https://www.tutorialspoint.com/unix_sockets/what_is_socket.htm)
* [cs.unc.edu](https://www.cs.unc.edu/~dewan/242/s07/notes/ipc/node27.html)