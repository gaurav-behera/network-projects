---
layout: page
title: Mini Project 2
permalink: /mini-projects/mp2
parent: Mini Projects
nav_order: 2
---

# Mini Project 2 : Introduction to XV-6

<!-- ## Operating Systems and Networks, Monsoon 2023 -->

## Deadline: 11:59pm 06 October 2023

---
# Specification **4 : Networking [ 30 marks ]**

**_UDP and TCP, but mostly TCP_**

## _Part A_ : Using library functions [ 12 marks ]

Implement the following within the `<mini-project2-directory>/networks/partA/basic` directory
1. TCP server program
2. TCP client program
3. UDP server program
4. UDP client program

The client program must send some text to the server and then receive some text from the server. 

You shall be awarded `1 mark per program` listed above _only_ if you check for all the errors that could come up, i.e., check the return status of all the relevant functions.

Now, for the rest of the 8 marks - you must make modifications to the programs listed above and add your submissions to `<mini-project2-directory>/networks/partA/rpc`

Here's the task - Implement rock, paper, scissor between two clients (4 marks for the UDP implementation and the other four for using TCP)
- Start server which listens for two clients on two different ports.
- Start two clients - clientA and clientB
- Users enter their decision (Rock, Paper or Scissors) in clientA and clientB.
- Server receives the decisions from clientA and clientB.
- Server deliberates and returns it's judgement to both the clients.
- Clients display the judgement ("Win", "Lost", "Draw")
- Implement a loop such that the clients are prompted for another game after the judgement (The next game starts only if both the clients say yes - handle this using the server)

_NOTE_: we are NOT expecting anything fancy here - using 0 for Rock (i.e., expecting the user to input 0 for rock), etc., is also fine.

Libraries you could use are - arpa/inet.h, sys/types.h, sys/socket.h, netinet/in.h

### Resources that you could refer to - 
1. [https://www.csd.uoc.gr/~hy556/material/tutorials/cs556-3rd-tutorial.pdf](https://www.csd.uoc.gr/~hy556/material/tutorials/cs556-3rd-tutorial.pdf) - slides on socket programming
2. [https://github.com/nikhilroxtomar/TCP-Client-Server-Implementation-in-C](https://github.com/nikhilroxtomar/TCP-Client-Server-Implementation-in-C) - TCP client and server in C using library functions (be wary as they haven't used `htons()`)
3. [https://github.com/nikhilroxtomar/UDP-Client-Server-implementation-in-C](https://github.com/nikhilroxtomar/UDP-Client-Server-implementation-in-C) - UDP client and server in C
4. man pages :)

## _Part B_ : Implement some TCP (?) functionality from scratch [ 18 marks ]

> Seems daunting but really isn't (read on)

We can't really ask you to implement the entire TCP/IP stack from scratch for about twenty marks (But, for the ones interested here's a repo on it - [https://github.com/saminiir/level-ip](https://github.com/saminiir/level-ip))

So, here's what you actually need to do - 

**Implement _some_ TCP functionality using UDP sockets**

_Seems hack-y? Very_. But, it's OSN not just N and the point of this course is to hopefully make you understand some stuff. 

Functionalities that you have to implement are (10 marks):
1. **Data Sequencing**: The sender (client or server - both should be able to send as well as receive data) must divide the data (assume some text) into smaller chunks (using chunks of fixed size or using a fixed number of chunks). Each chunk is assigned a number which is sent along with the transmission (use structs). The sender should also communicate the total number of chunks being sent [1]. After the receiver has data from all the chunks, it should aggregate them according to their sequence number and display the text.
2. **Retransmissions**: The receiver must send an ACK packet for every data chunk received (The packet must reference the sequence number of the received chunk). If the sender doesn't receive the acknowledgement for a chunk within a reasonable amount of time (say 0.1 seconds), it must resend the data. However, the sender shouldn't wait for receiving acknowledgement for a previously sent chunk before transmitting the next chunk [2].

    [1] Regardless of whether you use a fixed number of chunks
   
    [2] For implementation's sake, send ACK messages randomly to check whether retransmission is working - say, skip every third chunk's ACK. (Please _comment_ out this code in your final submission)

_Edit:_ You may simulate only one client and one server as there is no specification asking for demonstrating a connection between a client and a server.

To make your life simpler, the rest of the 8 marks is a report - 
1. How is **your** implementation of data sequencing and retransmission different from traditional TCP? (If there are no apparent differences, you may mention that) (3 marks)
2. How can you extend **your** implementation to account for [flow control](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#Flow_control)? You may ignore deadlocks. (5 marks)

Submit your implementation for the server and client in `<mini-project2-directory>/networks/partB`

---


# Guidelines:
1. Do not change the basic file structure given on Github Classroom.
2. No deadline extensions will be granted.

**Do NOT take codes from seniors or your batch mates, by any chance. We will extensively evaluate cheating scenarios along with the previous few year’s submissions.**

**Viva will be conducted during the evaluations, related to your code and also the logic/concept involved. If you’re unable to answer them, you’ll get no marks for that feature/topic that you’ve implemented.**