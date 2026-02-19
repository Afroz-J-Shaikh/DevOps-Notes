# Networking Fundamentals & Hands-on Checks

## OSI and TCP/IP Model

### OSI Model - 
OSI is a conceptual model that defines network communication. It consists of 7 layers where each layer performs a specific function.
* **Application L7** - User interaction (e.g., browser).
* **Presentation L6** - Data encryption/decryption, format conversion.
* **Session L5** - Establish/manage/terminate sessions.
* **Transport L4** - Reliable delivery (TCP/UDP).
* **Netwrok L3** - IP addressing, routing.
* **Data Link L2** - Error‑free node‑to‑node delivery.
* **Physical L1** - Hardware, cables, signals.

### TCP/IP Model - 
TCP/IP is practically used for providing communication between computers over the internet.

* **Application L4** - Combines OSI’s Application + Presentation + Session. 
* **Transport L3** - Same as OSI Transport.
* **Internet L2** - Same as OSI Network.
* **Netwrok access L1** - Physical + Data Link combined.

### Protocol Placement

* **HTTP, HTTPS, FTP, SMTP, DNS, DHCP, SSH** - Application layer
* **TCP, UDP** - Transport Layer
* **IP, ICMP, ARP** - Internet Layer
* **Ethernet, Wi-Fi** - Network Access layer

### Real Example

![snapshot](images/curl.png)

→ HTTP (Application) over TCP (Transport) over IP (Internet)

## Hands-on Checklist

* Identity : `hostname -I`

 **Observation:** Local private IP address is 10.84.212.222
 
![snapshot](images/ip.png)

* Reachability: `ping <target>`

 **Observation:** 0% packet loss with 4006ms average latency confirms good network connectivity.
 
![snapshot](images/ping.png)

* Path: `traceroute <target>`

 **Observation:** 30 hops max with 80.629 ms latency.
  Longer latency at hop 2 compared to others.
  
![snapshot](images/traceroute.png)

* Ports: `ss -tulpn` or `netstat -tulpn`

 **Observation:** Service - ssh. SSH is listening on port 22.
 
![snapshot](images/port.png)

* Name resolution: `dig <domain>` or `nslookup <domain>`

 **Observation:** Domain resolves to 142.250.70.100.
 
![snapshot](images/dig.png)

* HTTP check: `curl -I <http/https-url>`

 **Observation:** Received response HTTP/1.1 200 OK. Server successfully responded and the resource is available.
 
![snapshot](images/curl_I.png)

* Connections snapshot: `netstat -an | head`

 **Observation:** LISTEN: 5 entries (ports 631, 7071, 53, 54, 22).
 ESTABLISHED: 3 entries (all HTTPS connections).
 
![snapshot](images/netstat.png)

## Mini Task: Port Probe & Interpret

- SSH service on port 22

![snapshot](images/ss_ssh.png)

- Connection succeeded

![snapshot](images/nc.png)

**If not reachable :** 
- Check service status - `systemctl status ssh`
- Check logs - `journlctl -u ssh`
- Check firewall - `sudo ufw status`

## Reflection

- **Ping** command gives fastest signal if something is broken.
- DNS fails : It runs on application layer if DNS queries don’t resolve, the next logical layer to inspect is 
  the Transport layer (L4) and Internet layer (L3)
  
  -> dig, nslookup, ping, ss -tulpn
- HTTP 500 : It is application layer. Since you got response(500) it means internet and transport layers are fine.
  Check at Application layer.
  
  -> systemctl status service, journalctl -u service, tail -f /var/log/service/error.log
- Follow up checks in real incident :
    * Check firewall (`sudo ufw status`,`sudo iptables -L -n -v`)
    * Service helth check (`systemctl status <service>`)
    * Connectivity test (`curl -I http://<server-ip>:<port>`,`nc -zv <server-ip> <port>`)
