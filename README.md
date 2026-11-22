# 2c.SIMULATING ARP /RARP PROTOCOLS

## AIM
To write a python program for simulating ARP protocols using TCP.

## ALGORITHM:

## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.

## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.

## PROGRAM - ARP

## Client
```
import socket
s = socket.socket()
s.connect(('localhost', 8001))
ip = input("Enter IP Address: ")
s.send(ip.encode())
mac = s.recv(1024).decode()
print("MAC Address:", mac)
s.close()
```
## Server
```
import socket
s = socket.socket()
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s.bind(('localhost', 8001))
s.listen(1)
print("ARP Server waiting for client...")
c, addr = s.accept()
print("Client connected")
ip = c.recv(1024).decode()
print("Received IP Address:", ip)
arp_table = {
    "10.104.8.61": "FC:6D:77:8A:DF:F4",
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02"
}
if ip in arp_table:
    mac = arp_table[ip]
else:
    mac = "IP Address not found"
c.send(mac.encode())
print("MAC Address:", mac)
c.close()
s.close()
```
## OUPUT - ARP

## Client

<img width="1361" height="153" alt="image" src="https://github.com/user-attachments/assets/d6a8f13c-fd95-4e9c-912f-e04b71b8fbe5" />

## Server

<img width="1359" height="187" alt="image" src="https://github.com/user-attachments/assets/9a54b837-ea5b-4039-9397-fc594079d603" />

## PROGRAM - RARP

## Client
```
import socket
s = socket.socket()
s.connect(('localhost', 8002))
mac = input("Enter MAC Address: ").strip().upper()
s.send(mac.encode())
ip = s.recv(1024).decode()
print("IP Address:", ip)
s.close()
```
## Server
```
import socket
s = socket.socket()
s.connect(('localhost', 8002))
mac = input("Enter MAC Address: ").strip().upper()
s.send(mac.encode())
ip = s.recv(1024).decode()
print("IP Address:", ip)
s.close()
```
## OUPUT -RARP

## Client

<img width="1342" height="108" alt="image" src="https://github.com/user-attachments/assets/5d5fe2b2-7c90-44eb-82e2-80e2de01bc0d" />

## Server

<img width="1305" height="178" alt="image" src="https://github.com/user-attachments/assets/9480c95b-bf44-458d-9ec9-f05b64d0f6fe" />

## RESULT

Thus, the python program for simulating ARP protocols using TCP was successfully executed.
