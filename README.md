
# Wireshark Fundamentals Lab



## 🛠️ Step 1 — Install Wireshark

Watch me doing Step 1-3:
[![wireshark1](https://github.com/user-attachments/assets/54e9c46e-435c-40e9-8083-f0a7ad90ea8a)](https://www.loom.com/share/b13057aa38544f2b940c8c2e0d9d6ba6)

Set up the packet analyzer you’ll use throughout the lab.

- Go to **wireshark.org/download.html**
- **Download** the installer for your operating system (Windows, macOS, or Linux)
- **Install** using default settings — no license, trial, or account required



## 🚀 Step 2 —  Run Your First Packet Capture

Get familiar with the Wireshark interface and live traffic view.

- **Launch** Wireshark
- On the welcome screen, review the list of **network interfaces**
- Double click the interface with **the most activity** (Ethernet or Wi Fi)
- Watch packets populate in **real time**
- Open a browser and visit any website to generate traffic
- After ~30 seconds, click the red **Stop** button to end the capture



## 🔍 Step 3 - Use Essential Display Filters

Learn to isolate specific traffic types using Wireshark’s filter bar.

- Type a **filter** (e.g., dns, tcp, icmp) into the filter bar
- Press **Enter** to apply it
- Observe how the packet list updates instantly
- Practice filtering by protocol, IP, and port



## 📝  Step 4 - Capture a DNS Lookup

Trigger a **DNS query manually** and analyze the request and response.

- Start a capture on your active interface
- Open a terminal, on Windows search for: **Command Prompt**
- Run: **nslookup google.com**
- **Stop** the capture
- Apply filter: **dns**
- Locate the Standard query A google.com packet
- Locate the Standard query response packet
- Expand the DNS response to view the returned IP address



## 🔗 Step 5 - Observe the TCP Three Way Handshake

Identify the **SYN → SYN ACK → ACK** sequence that establishes a TCP connection.

- Start a **new capture**
- Browse to **http://zero.webappsecurity.com/login.html** (HTTP makes the handshake easier to see)
- **Stop** the capture
- Run **nslookup zero.webappsecurity.com** to get the server IP
- Apply filter: **tcp and ip.addr == <IP>** (In my case was: tcp and ip.addr == 54.82.22.214 )
- Find the **three handshake** packets:
    - SYN — client initiates connection
    - SYN, ACK — server acknowledges
    - ACK — connection established



## 🔍 Step 6 - Identify Cleartext Credentials (HTTP)

Analyze an HTTP POST request to understand why HTTPS is essential.

- Only perform this on systems you own or have permission to test
- Start a capture
- Submit a login form over HTTP (not HTTPS) using test credentials
- Stop the capture
- Apply filter: http.request.method == POST
- Select the POST packet and expand HTML Form URL Encoded
- Observe the username and password in plaintext



## 🔁 Step 7 - Follow a Full TCP Stream

Reconstruct an entire HTTP conversation between client and server.

- Capture traffic while visiting an HTTP site
- Select any HTTP packet
- Right click → Follow → TCP Stream
- Review the reassembled conversation:
    - Red = client request
    - Blue = server response



## 📘 Step  8 - Save and Export Captures

Preserve your work for later analysis or portfolio use.

- Save full capture: File → Save As → .pcapng
- Export only filtered packets: File → Export Specified Packets → Displayed
- Reopen captures anytime: File → Open
- Command line capture (tshark):
  Code
  tshark -i eth0 -w capture.pcapng -c 1000



## 📝 Step  9 - Verify Your Skills

Self Check: Confirm you can perform each core Wireshark task without guidance.

- Capture and filter DNS traffic; match query/response IDs
- Identify a TCP three way handshake and explain each flag
- Apply filters from memory: protocol, IP, port
- Follow a TCP stream and read the full HTTP exchange
- Save, close, and reopen a capture file successfully



