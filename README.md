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
s.connect(('localhost', 8000))
ip = input("Enter IP address: ")
s.send(ip.encode())
mac = s.recv(1024).decode()
print("MAC Address:", mac)
s.close()
```
## Server
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("ARP Server is running...")
# IP-MAC address mapping
arp_table = {
    "192.168.1.10": "AA:BB:CC:DD:EE:01",
    "192.168.1.20": "AA:BB:CC:DD:EE:02",
    "192.168.1.30": "AA:BB:CC:DD:EE:03"
}
while True:
    c, addr = s.accept()
    print("Client connected:", addr)
    ip = c.recv(1024).decode()
    if ip in arp_table:
        mac = arp_table[ip]
        c.send(mac.encode())
    else:
        c.send("IP address not found".encode())
    c.close()
```
## OUPUT - ARP

## Client


## Server


## PROGRAM - RARP

## Client
```
import socket
s = socket.socket()
s.connect(('localhost', 8001))
mac = input("Enter MAC address: ")
s.send(mac.encode())
ip = s.recv(1024).decode()
print("IP Address:", ip)
s.close()
```
## Server
```
import socket
s = socket.socket()
s.bind(('localhost', 8001))
s.listen(5)
print("RARP Server is running...")
# MAC-IP address mapping
rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.10",
    "AA:BB:CC:DD:EE:02": "192.168.1.20",
    "AA:BB:CC:DD:EE:03": "192.168.1.30"
}
while True:
    c, addr = s.accept()
    print("Client connected:", addr)
    mac = c.recv(1024).decode().upper()
    if mac in rarp_table:
        ip = rarp_table[mac]
        c.send(ip.encode())
    else:
        c.send("MAC address not found".encode())
    c.close()
```
## OUPUT -RARP

## Client


## Server


## RESULT

Thus, the python program for simulating ARP protocols using TCP was successfully executed.
