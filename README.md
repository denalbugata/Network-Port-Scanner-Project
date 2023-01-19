<h1>Network Scanner Project</h1>


<h2>Description</h2>
This script is a basic network and port scanner that uses Linux and Python. It first imports the socket module and then defines the target IP and port range that will be scanned. It then iterates through each port in the range, starting from start_port to end_port+1. For each port, it creates a socket object and sets a timeout value for the socket. It attempts to connect to the target IP on the current port using the connect_ex() function. If the connection is successful, it prints the port number. The script then closes the socket. This script will scan the target IP for open ports within the specified range using the socket library in Python, which allows for low-level network communication.
<br />



<h2>Environments Used </h2>

- <b>Windows 11</b> 

<h2>Program Code:</h2>

```python
# Step 1: Import the necessary modules
import socket

# Step 2: Define the target IP and port range
IP = "192.168.1.1"
start_port = 1
end_port = 100

# Step 3: Iterate through each port in the range
for port in range(start_port, end_port + 1):
    # Step 3.1: Create a socket object
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    # Step 3.2: Set the timeout value for the socket
    sock.settimeout(5)
    # Step 3.3: Attempt to connect to the target IP on the current port
    result = sock.connect_ex((IP, port))
    # Step 3.4: If the connection is successful, print the port number
    if result == 0:
        print("Port {}: Open".format(port))
    # Step 3.5: Close the socket
    sock.close()

```
