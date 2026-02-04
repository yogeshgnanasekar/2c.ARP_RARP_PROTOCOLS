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
    s = socket.socket()
    s.bind(('localhost', 8000))
    s.listen(5)
    print("Server is listening...")

  c, addr = s.accept()
  print(f"Connection established with {addr}")

  address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
  }

  while True:
    ip = c.recv(1024).decode()

    if not ip:  
         break

    try:
        mac = address[ip]  # Get the MAC address for the IP
        print(f"IP: {ip} -> MAC: {mac}")
        c.send(mac.encode())  
    except KeyError:
        print(f"IP: {ip} not found in ARP table.")
        c.send("Not Found".encode())
    c.close()
    s.close()

    c = socket.socket()
    c.connect(('localhost', 8000))

    while True:
      ip = input("Enter IP address to find MAC (or type 'exit' to quit): ")

      if ip.lower() == "exit":  
        break

     c.send(ip.encode())
     mac = c.recv(1024).decode()
     print(f"MAC Address for {ip}: {mac}")
    c.close()


## OUPUT -RARP
<img width="970" height="485" alt="Screenshot 2026-02-04 193814" src="https://github.com/user-attachments/assets/fe4a94e2-e5a4-404f-9d94-a0dcf192af6f" />
<img width="701" height="416" alt="Screenshot 2026-02-04 193821" src="https://github.com/user-attachments/assets/126f13d7-080e-46d6-b631-aef7e2783be3" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
