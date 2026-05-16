# Nmap Advanced Port Scan 
---

### In previous we saw the Host discovery and Some Basic port scan ,now in this repo we are goin to see some Advanced port scans as below.
- TCP null scan,FIN scan,XMAS scan.
- TCP maimon scan
- TCP ACK,Window and Custom scan
- Spoofing and decoys
- Frangmented packets
- Ideal and zombie scan.

---

# 1. TCP Null scan :
- As the name suggest Null scan does not set any flag.all 6 flags are set to zero
- command is : nmap -sN target
- When a TCP packet with no flag reaches to target it doe not trigger any response form target.
- Lack of response from the server indicates that either port is open or the firewall is blocking the response and reply
- wwhen TCP packet with no flag is sent to server an closed port will response with RST flag.
- SO lack of RST flages are considered to determine port is open.
