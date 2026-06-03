# Lab 1.1 Findings
The screenshots related to this lab can be found [here](Lab1.1.PC_2_VM_Findings.docx)

## My VM Details
- Provider: OCI (Oracle Cloud Infrastructure)
- Region: ap-mumbai-1
- OS: Canonical Ubuntu 24.04


## Experiment Results

### Ping to 8.8.8.8
- Average RTT: 1.203 ms
- TTL value observed: 120
- What does TTL tell us about the path?

  TTL value essentially tells us how many hops(routers) that a packet needs to go through before it reaches its destination. Generally, TTL is assigned at the beginning of transmission, typically based on the OS, like 128 in Windows or 64 in Linux or macOS. Here, the observed TTL value is 120, meaning that from the initial TTL value that was assigned as 128, due to me being on a Windows system, it has utilised 8 hops or has been "routed" through 8 routers to reach its destination from the source, that is the VM from the Google DNS server. The math is simple, subtract the observed TTL value from the generic assigned TTL value to get the number of hops(routers) utilised (128-120=8). {Here, I assumed assigned TTL as 128 even though there is no clear indication, as TTL value can only decrease, and not actually increase, and hence, the 64 option for Linux/macOS automatically gets removed from the list, since 128 is greater than 64. Additionally, with the value being expected at 112 or similar(~16 hops), it goes to show that the pathway from the Google DNS server (specifically 8.8.8.8) to my VM is highly efficient pathway. Also, the different TTL of 115 in the ping targeting specifically google.com, shows that it has pinged a different IP address (specifically 142.250.246.139), which is not as efficient as the earlier path, as it utilises 13 hops in this case, which goes to show that these two servers are at different 'distances' from my VM, speaking in terms of networks.}

### Traceroute to google.com
- Number of hops: 14 hops to reach the final destination
- Any * * * hops? At which hop number?

  Yes, hops 8, 9, 10, 11, 12, and 13 showed "* * *".

### DNS Comparison
- Result from default DNS (127.0.0.53):

Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:   google.com
Address: 142.250.146.138
Name:   google.com
Address: 142.250.146.102
Name:   google.com
Address: 142.250.146.139
Name:   google.com
Address: 142.250.146.113
Name:   google.com
Address: 142.250.146.101
Name:   google.com
Address: 142.250.146.100
Name:   google.com
Address: 2404:6800:4000:100c::71
Name:   google.com
Address: 2404:6800:4000:100c::8b
Name:   google.com
Address: 2404:6800:4000:100c::8a
Name:   google.com
Address: 2404:6800:4000:100c::64

- Result from 1.1.1.1:

Server:         1.1.1.1
Address:        1.1.1.1#53

Non-authoritative answer:
Name:   google.com
Address: 192.178.173.139
Name:   google.com
Address: 192.178.173.100
Name:   google.com
Address: 192.178.173.102
Name:   google.com
Address: 192.178.173.101
Name:   google.com
Address: 192.178.173.113
Name:   google.com
Address: 192.178.173.138
Name:   google.com
Address: 2404:6800:4000:100e::71
Name:   google.com
Address: 2404:6800:4000:100e::64
Name:   google.com
Address: 2404:6800:4000:100e::66
Name:   google.com
Address: 2404:6800:4000:100e::8b

- Are they different? Why might they differ?

  Yes, they are different. Google runs multiple servers to respond to requests, which make sure that even if one server fails to respond or crashes, other servers can pick up and service the traffic that visits the servers. In the first command, the result for the default server 127.0.0.53 returns a range of IPs(142.250.146.x), which goes to show that on requesting the Google DNS server, it automatically redirected me to that specific ip range's server, as it computed it to be the 'nearest' and most easily accessible server, considering the 'location' of the originating request. In the second command, I sent a request from the 1.1.1.1 server, which belongs to Cloudflare. Cloudflare doesnt share the request location data, so the Google DNS server automatically assigned a server that was 'nearer' to the Cloudflare 1.1.1.1 IP server, so the two commands, although I am requesting the same entity, the servers providing the service are entirely different, leading to a difference in the results for the nslookup command.

### google.com TLS Certificate
- Issuer: C = US, O = Google Trust Services, CN = WR2
- Expiry date: Jul 30 15:51:25 2026 GMT
- TLS version used: TLSv1.3
