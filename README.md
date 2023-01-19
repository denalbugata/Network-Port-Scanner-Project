<h1>Network Scanner Project</h1>


<h2>Description</h2>
This script uses the nmap command-line tool to perform a ping scan and a port scan on the given network range. The script first uses nmap to perform a ping scan, which simply checks if hosts are up. It then filters the output of nmap to a file hosts_up.txt that includes only the IP addresses of the hosts that are up. Next, it iterates through each host that is up, and performs a full port scan on each host using nmap. Finally, the script prints the open ports for each host and removes the temp files created.
<br />



<h2>Environments Used </h2>

- <b>Windows 11</b> 

<h2>Program Code:</h2>

```python
# Import the necessary libraries
import os
import socket

# Clear the terminal
os.system('clear')

# Get the network range to scan from the user
network_range = input("Enter the network range to scan (e.g. 192.168.1.0/24): ")

# Use the nmap library to perform a ping scan on the given network range
# The -sn flag tells nmap to perform a "ping scan", which simply checks if hosts are up
# The -oG flag tells nmap to output the results in "grepable" format, which makes it easier to parse the results
ping_scan = os.system('nmap -sn -oG - ' + network_range + ' | grep Up > hosts_up.txt')

# Open the file that contains the hosts that are up
with open('hosts_up.txt', 'r') as f:
    hosts_up = f.readlines()

# Initialize an empty list to store the open ports for each host
open_ports = {}

# Iterate through each host that is up
for host in hosts_up:
    # Extract the IP address of the host from the nmap output
    ip_address = host.split(" ")[1]

    # Use the nmap library to perform a port scan on the host
    # The -p flag tells nmap which ports to scan
    # The -oG flag tells nmap to output the results in "grepable" format, which makes it easier to parse the results
    port_scan = os.system('nmap -p 1-65535 -oG - ' + ip_address + ' | grep open > ports_open.txt')

    # Open the file that contains the open ports for the host
    with open('ports_open.txt', 'r') as f:
        ports_open = f.readlines()
        
    # Add the open ports to the list
    open_ports[ip_address] = ports_open

# Print the open ports for each host
for host, ports in open_ports.items():
    print(host + ": " + str(ports))
    
# remove the temp files created
os.system('rm ports_open.txt hosts_up.txt')


```
