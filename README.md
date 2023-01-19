<h1>Network Scanner Project</h1>


<h2>Description</h2>
This script uses a combination of ICMP pings and TCP connection attempts to identify active hosts and open ports on a given network range. It uses Python's built-in socket library to handle the network communication. The NetworkScanner class has several methods: ping_host, scan_ports, and start_scan. start_scan method is used to start the scanning process, which will first check if the host is up using ICMP ping and if host is up then it will scan for all open ports.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Python</b> 

<h2>Environments Used </h2>

- <b>Windows 11</b> 

<h2>Program Code:</h2>

```python
import socket
import struct
import threading
import time

class NetworkScanner:
    def __init__(self, target_ip):
        self.target_ip = target_ip
        self.open_ports = []

    def ping_host(self, ip):
        """
        Sends a ping request to a host using the ICMP protocol.
        Returns True if the host is up, False otherwise.
        """
        try:
            sock = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_ICMP)
            sock.settimeout(2)
            sock.sendto(b'', (ip, 1))
            sock.recvfrom(1024)
            return True
        except:
            return False

    def scan_ports(self, ip):
        """
        Scans all ports on a host to check if they are open.
        """
        for port in range(1, 65535):
            sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            sock.settimeout(2)
            result = sock.connect_ex((ip, port))
            if result == 0:
                self.open_ports.append(port)
            sock.close()

    def start_scan(self):
        """
        Starts the network scan.
        """
        print(f'[*] Starting scan of IP range {self.target_ip}')
        start_time = time.time()
        for i in range(1, 255):
            ip = f'{self.target_ip}.{i}'
            if self.ping_host(ip):
                print(f'[*] Host {ip} is up')
                self.scan_ports(ip)
                print(f'[*] Open ports on host {ip}: {self.open_ports}')
                self.open_ports.clear()
        end_time = time.time()
        print(f'[*] Scan completed in {end_time - start_time} seconds')

scanner = NetworkScanner("192.168.1")
scanner.start_scan()
```
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
