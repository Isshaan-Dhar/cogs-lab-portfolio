# Lab 1.3 Findings: WireGuard VPN & ZTNA Principles

### 1. Active Peer Handshake
The two screenshots below show the outputs from the 'wg show' commands, that I ran on both the VMs. The keys are matching and that a secure connection is established properly, which is shown by the recent handshake timestamps and the activity of data transfer.

**VM1 (Gateway/Server) Handshake:**

![VM1 Handshake](../../screenshots/Screenshot%202026-05-27%20075116.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------


**VM2 (Agent/Client) Handshake:**

![VM2 Handshake](../../screenshots/Screenshot%202026-05-27%20075130.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------


### 2. Encrypted Tunnel Connection
From VM2, I pinged the internal WG IP of VM1 (10.0.0.1). Also, we can see that there is a 0% packet loss, which shows us that it is routing perfectly through the 10.0.0.0/24 subnet and not other public unstable pathways.

![VM2 Ping Test](../../screenshots/Screenshot%202026-05-27%20075157.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------


### 3. E2E Encryption Verification
A tcpdump command (packet capture) on VM1 (ens3, not eth0) port 51820 shows only UDP packets. The ping requests are totally encapsulated and encrypted, shown only as 148-byte and 32-byte UDP transfers show unreadability over public web.

![Encrypted Traffic Capture](../../screenshots/Screenshot%202026-05-27%20075436.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------------------------------


**1. VM2 (VPN CLIENT) - ZTNA AGENT:** In WG, VM2 is a peer starting a tunnel. In ZTNA, the equivalent is the Agent, which is installed on the user's device. The agent established secure tunnel, but also continuously checks for device posture (OS Version, security status etc.) before actually allowing the connection.

**2. VM1 (VPN SERVER) - ZTNA GATEWAY:** In WG, VM1 is the listener and router for 10.0.0.0/24 network. The ZTNA Gateway is its parallel, but instead of a direct server, it acts as a reverse proxy, acting as a security guard that protects the client's applications from public access.

**3. UDP PORT 51820 TUNNEL - ZTNA 'MICROTUNNEL':** WG will create a big, standard tunnel, for all traffic between two IPs. Parallel to this is ZTNA's 'microtunnels' which are small tunnels for each different applications, which are kept 'alive' for only the duration of a session.

**4. MY PC (ESSENTIALLY ME) - ZTNA CONTROLLER:** I had to manually configure the firewall using ufw commands, paste the keys for each machine onto the other and other technical duties. In ZTNA, these duties are carried out by the Controller, which automates the entire process for potentially thousands of simultaneous users at the same time, saving the time and effort that would have had to been invested into the manual configuration of so many users.

**5. PUBLIC/PRIVATE KEY PAIRS - IDENTITY CERTIFICATES AND IdP:** So,here I had to manually copy and paste the keys into each VM, for trusted connections to be implemented. This is replaced by ZTNA with Identity Certificates using Public Key Infrastructure (PKI), and the concept of Identity Provider (IdP).
