<h1>Network Scanner Project</h1>


<h2>Description</h2>
This script is a basic network and port scanner that uses Linux and Python. It first imports the socket module and then defines the target IP and port range that will be scanned. It then iterates through each port in the range, starting from start_port to end_port+1. For each port, it creates a socket object and sets a timeout value for the socket. It attempts to connect to the target IP on the current port using the connect_ex() function. If the connection is successful, it prints the port number. The script then closes the socket. This script will scan the target IP for open ports within the specified range using the socket library in Python, which allows for low-level network communication.
<br />



<h2>Environments Used </h2>

- <b>Windows 11</b> 

<h2>Program Walkthrough:</h2>

<b>Step 1: This line imports the socket module, which provides a low-level core networking service. It is used to create, bind, and listen to sockets, as well as to make connections to other hosts using sockets.</b>

```python
import socket
```
<b>Step 2: This line defines the variable IP and assigns it the value "192.168.1.1" which is the target IP that the script will try to connect to.</b>

```python
IP = "192.168.1.1"
```
<b>Step 3: This line of code defines the start_port and end_port variables, which are used to define the range of ports that the script will iterate through.</b>

```python
start_port = 1
end_port = 100
```
<b>Step 4: This line of code is a for loop that iterates through each port in the defined range. The loop variable 'port' is assigned the value of the current port in the range on each iteration.</b>

```python
for port in range(start_port, end_port + 1):
```
<b>Step 5: This line of code creates a socket object using the socket.socket() method, where the first parameter is the address family (AF_INET) and the second parameter is the type of socket (SOCK_STREAM).</b>

```python
sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```
<b>Step 6: This line sets the timeout value for the socket to 5 seconds.</b>

```python
sock.settimeout(5)
```
<b>Step 7:This line attempts to connect to the target IP on the current port, and assigns the returned result to the variable 'result'.</b>

```python
result = sock.connect_ex((IP, port))
```
<b>Step 8: This line of code checks if the connection is successful by checking if the 'result' variable is equal to 0.</b>

```python
if result == 0:
```
<b>Step 9: If the 'if' statement in the previous line is true, this line of code will execute, printing the message "Port {}: Open" with the current port number.</b>

```python
print("Port {}: Open".format(port))
```
<b>Step 10:This line of code closes the socket.</b>

```python
sock.close()
```
<b>The final result should look like this:</b>

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
