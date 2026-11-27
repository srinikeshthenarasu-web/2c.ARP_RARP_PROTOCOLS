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
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
CLIENT:
```
import socket
s = socket.socket()
s.connect(('localhost', 12345))
ip = input("Enter IP Address: ")
s.send(ip.encode())
mac = s.recv(1024).decode()
print("MAC Address:", mac)
s.close()
```
SERVER:
```

import socket
s = socket.socket()
s.bind(('localhost', 12345))
s.listen(1)
print("ARP Server waiting for client...")
c, addr = s.accept()
arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}
ip = c.recv(1024).decode()
mac = arp_table.get(ip, "MAC Address not found")
c.send(mac.encode())
print("IP Address:", ip)
print("MAC Address:", mac)
c.close()
s.close()
```
## OUPUT - ARP
<img width="881" height="202" alt="Screenshot 2026-11-27 084800" src="https://github.com/user-attachments/assets/064e25c7-3cd5-4106-822a-2cc074d2c925" />

## PROGRAM - RARP
CLIENT:
```
import socket
s = socket.socket()
s.connect(('localhost', 12346))
mac = input("Enter MAC Address: ")
s.send(mac.encode())
ip = s.recv(1024).decode()
print("IP Address:", ip)
s.close()
```
SERVER:
```
import socket
s = socket.socket()
s.bind(('localhost', 12346))
s.listen(1)
print("RARP Server waiting for client...")
c, addr = s.accept()
rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}
mac = c.recv(1024).decode()
ip = rarp_table.get(mac, "IP Address not found")
c.send(ip.encode())
print("MAC Address:", mac)
print("IP Address:", ip)
c.close()
s.close()
```
## OUPUT -RARP
<img width="1468" height="148" alt="Screenshot 2026-11-20 083431" src="https://github.com/user-attachments/assets/a1ca0365-9086-425c-95e3-6c1ed5de49d1" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
