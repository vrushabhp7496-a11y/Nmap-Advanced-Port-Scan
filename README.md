# Nmap Advanced Port Scan 
---

### In previous we saw the Host discovery and Some Basic port scan ,now in this repo we are goin to see some Advanced port scans as below.
- TCP null scan,FIN scan,XMAS scan.
- TCP ACK,Window and Custom scan
- Spoofing and decoys
- Frangmented packets
- Ideal and zombie scan.

---

# 1.1 TCP Null scan :
- As the name suggest Null scan does not set any flag.all 6 flags are set to zero
- command is : nmap -sN target
- When a TCP packet with no flag reaches to target it doe not trigger any response form target.
- Lack of response from the server indicates that either port is open or the firewall is blocking the response and reply
- wwhen TCP packet with no flag is sent to server an closed port will response with RST flag.
- SO lack of RST flages are considered to determine port is open.

---

# 1.2 TCP FIN Scan : 
- The TCP FIN scan sends Packet set with FIN Flag.
- command is : nmap -sF target
- Similar to TCP Null scan no response is sent if port is open heance nmap cannot determine either port is open or firewall is blocking it
- Similar to TCP null scan when FIN packet is sent and response with RST gets shows taht p[ort is closed.
- Also some firewall drop the packet without sending the RST flag.


---

# 1.3 XMAS scan : 
- This scan sets the flag FIN,PSH,URG at same time.
- command is nmap -sX target
- similar to null and FIN scan if RST packet is recieve the port is closed and no response shows port is either open or filtered by firewall.

---

# 2.1 TCP ACK scan : 
- As the name suggest this scan sends packet set with ACK flag.
- command is : nmap -sA target.
- This scan dosent specify that port is open or closed it only clears taht port is filtered or unfiltered.
- If server response with no flag it means target is filtered or firewall is blocking .
- If server response with RST flag it means it is unfiltered or no firewall is present.
- It also helps to determine us that firewall is stateless or statefull
- Stateless firewall always allows ACK packet.
- Some firewall blocks the ACK packet and heance no response is obtained .

---

# 2.2 Window scan :
- This is as same as TCP ACK scan .
- A flag with ACK set is sent to target.
- Command is : nmap -sW target.
- Target response with RST packet.
- Nmap examins window size of this RST packet and determine weather port is open or closed
- If window size is zero then port is closed and window size is non zero port is open.

---

# 2.3 Custom Scan :
- If you want to scan with new TCP flag combination you can use this scan
- command is : --scanflag RSTSYNFIN
- Here you can set RST,SYN,FIN Flag at same time.
- This is the invalid combination for open port and heance any port wont response this
- But closed port wll response this with RST flag set.
- This type of scan can be used to scan port when Firewall is blocking previous methods of scanning.


---

# 3. Decoy or spoofing :
- In some system we can use spoofed IP address to scan network
- This type of scan hide real ip address of the attacker
- This will use Multiple ip address to scan server including Real and fake ip address.
- Target system responds to each and every IP address without knowing which is real and which is fake.
- This typpe is used when we are scanning very secured network,Confuse IDS system.
- This scan type is relatively slow because it uses too many ip address
- Many firewall identify the decoy and blocks them.
- Spoofed IP address scanning is only used when there is no need of response ass DDOS attacks
- In spoofing the response is sent to Fake ip address
- Command for Decoy ip adrress scan is : nmap -D 10.0.0.1,10.0.0.2,10.0.0.3,ME 192.168.1.1
- Command for spoofed ip address is : nmap -S 10.0.0.5 -e eth0 192.168.1.1

---

# 4. Fragmented Packets :
- Nmap provides fragmentation of data to scan the port
- command is : nmap -f 192.168.1.1
- -f splits the data into 8 bytes.
- -ff splits the data into 16 bytes.
- This scan is used to bypass the firewall.
- It is relatively slow.

---

# 5. Ideal/Zombie scan :
- In this scan attacker uses an weak or vulnerable ip address to scan target system.
- Heance Attacker using third ip address to scan target he remains stealthy or undetectable.
- Firstly attacker sends SYN/ACK packet to zombie machine and machine response with RST flag with containing its ip address.
- Attacker used this ip address to send TCP SYN on target machine
  1. If the target port is closed it send RST flag to ideal machine and ideal machine does not respond by itself.
  2. If the target port is open it sends SYN/ACK flag to ideal machine and ideal machine sends RST flag with incrimented id
  3. If the target machine is behind the firewall it does not respond with any flag.

- For zombie scan following consideration must be checked :
  1. IP ID should be incremental
  2. Zombie machine should be ideal.
  3. Zombie machine should reach the target system

---

### By Completing this repositery we have learned Nmap advanced port scan topic.
