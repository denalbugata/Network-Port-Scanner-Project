<h1>Network Scanner Project</h1>


<h2>Description</h2>
This code uses the os library to run command line functions and the nmap library to scan open ports on online hosts. It takes an IP range as input and performs a network scan to identify all active hosts within that range. It uses the ping command to check if a host is online, and the nmap library to scan open ports on online hosts. It also calculates and print the total scan time.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Python</b> 

<h2>Environments Used </h2>

- <b>Windows 11</b> 

<h2>Program Code:</h2>

```python
import os  # Importing the os library to run command line functions
import socket  # Importing the socket library to get information about network connections

def network_scanner(ip_range):
    """
    This function takes an IP range as input and performs a network scan to identify all active hosts within that range
    """
    # Clear the terminal screen
    os.system("clear")

    # Get current time for calculating total scan time
    start_time = datetime.now()

    # Use the ping command to check if a host is online
    online_hosts = []  # list to store online hosts
    for host in range(1,255):
        ip = ip_range + str(host)  # construct the IP address to scan
        response = os.system("ping -c 1 " + ip + " > /dev/null")  # send a single ping packet and redirect output to null
        if response == 0:  # if the return code is 0, the host is online
            online_hosts.append(ip)
            print(ip + " is online")

    # Use the nmap library to scan open ports on online hosts
    open_ports = {}  # dictionary to store open ports for each host
    for host in online_hosts:
        open_ports[host] = []  # initialize empty list for open ports of current host
        nm = nmap.PortScanner()  # create nmap object
        nm.scan(host, '1-1024')  # scan host on all ports between 1 and 1024
        for port in nm[host].all_tcp():  # iterate through all TCP ports
            if nm[host]['tcp'][port]['state'] == 'open':  # if the port is open
                open_ports[host].append(port)  # add the port to the list for the current host
                print(host + ": " + str(port) + " open")

    # Get current time again for calculating total scan time
    end_time = datetime.now()

    # Calculate and print total scan time
    total_time = end_time - start_time
    print("Scan completed in: " + str(total_time))

# Example usage
network_scanner("192.168.1.")

```
