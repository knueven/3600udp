3600udp
=======

A transport protocol for transmitting data reliably and in-order.

Developed on: 
Linux 3.13.0.24 (Ubuntu 14.04)
with gcc version 4.8.2

To install/run:
- Copy source files (3600recv.c, 3600send.c, and 3600sendrecv.c/h and the Makefile) into a directory
- make all;
- ./3600recv
- ./3600send [ip:port] and feed data into STDIN

Features/Implementation
-----------------------

Our code uses a variable window and timeout to detect and handle problems efficiently. An exponential average of the round-trip times of each (successful) data packet is used to keep timeouts as accurate as possible.

Other features of our implementation include:

- Slow Start/Congestion Avoidance

Our transport protocol has two phases of transmission to make efficient use of the network, slow start and congestion avoidance. In slow-start, the windows size scales up quickly, doubling with each successful round of ACKs. If duplicate ACKs are received or a timeout is reached, the window size is halved and congestion avoidance scales up the window size slowly.

- Checksum

Our code assures the integrity of each data packet by creating a checksum at the sender (8-bit 1's complement sum of the rest of the header as well as the packet's data) which is then checked by the receiver.

