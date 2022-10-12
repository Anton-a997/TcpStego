# TcpStego
A demonstration program for covert data transmission via TCP/IP header fields

The program was developed to test the feasibility of covert data transmission. Service fields of the TCP and IPv4 protocols were used for covert transfer.

On the sender side, plaintext is encrypted using the AES algorithm. The ciphertext is split into 8-byte data blocks. After that, the Type of Service field of the IP header is set to 0, and the size of the encrypted data in bytes is placed into the Identification field of the first IP packet header; the first 8 bytes of data are placed as the Timestamp option value in the TCP options header field.
The following structure is then used for covert data transmission:
- The IP header ID field is assigned the sequence number of each encrypted data block (8 bytes). This identification allows the receiver to correctly assemble the data in the order it was sent;
- The IP header Type of Service field is set to 1;
- 8 bytes of data are placed in the TCP options header field.

SYN and FIN flags in the TCP packet header are used to identify the beginning and end of a communication session between the sender and receiver.
Data is transmitted to a predefined TCP port. For each packet, the receiving side notifies the sender that the next block of data can be transmitted by responding with an ACK packet. This is done to mimic a normal TCP connection between client and server.

A new TCP connection is established for each message. Each new connection is opened and closed properly, so it does not trigger any warnings during traffic analysis in Wireshark.

https://user-images.githubusercontent.com/88583217/195650704-4b0ee618-d2a2-4032-b96e-ccaf3b6bc935.mp4
