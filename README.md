# Cybersecurity Portfolio

Hands-on cybersecurity learning journey — notes, labs, and projects, building toward an entry-level cybersecurity career.

## Projects

### 1. How the Internet Works — My Notes
- Ports — A port is like a specific door on your computer, used for a specific type of traffic. For example, port 80 is for non-encrypted information, like a postcard, and port 443 is for encrypted information, like a postcard sealed within a protected private envelope that secures the information.
- Public vs Private IP — My private IP is for my individual devices, and my public IP is like the main address for the household.
- DNS — DNS is like a phonebook that turns a name like google.com into an IP address.

### 2. Setting Up a Kali Linux Lab & Core Command-Line Skills
I set up a Kali Linux virtual machine using VirtualBox, giving me a safe, isolated environment to practice security tools without affecting my main computer. Kali is the operating system most SOC analysts and security professionals use day-to-day.

I learned core Linux navigation commands: `pwd` (shows current location), `ls` (lists files/folders), `cd` (changes folder), and `whoami` (shows current user). I also learned to create, view, and edit files using `touch`, `cat`, and `nano`.

Finally, I learned about file permissions, using `ls -l` to see who can read, write, or execute a file, and `chmod` to change those permissions. This matters for security because mis-configured permissions (files left open to everyone) are a real vulnerability attackers look for.

### 3. Analyzing Network Traffic with Wireshark
I installed Wireshark and used it to capture live network traffic from my own device in real time. I learned to use display filters to isolate specific types of traffic: `tls` to show only encrypted (HTTPS) traffic, `ip.addr == [IP]` to isolate all traffic to/from a specific address, and `http` to find unencrypted traffic.

Most of my everyday browsing traffic was encrypted (TLS), while the small amount of unencrypted HTTP traffic I found was routine background activity, such as Windows checking certificate validity and software updates, not sensitive personal data.

This exercise reinforced why HTTPS matters in practice: if sensitive information (like a login form) were sent over unencrypted HTTP instead, anyone intercepting the traffic could read it in plain text. This is the kind of traffic inspection SOC analysts use to investigate suspicious network activity.

**DNS Lookup in Practice:** I looked up how a website name gets converted into a connection. Using Wireshark, I found a DNS query for `claude.ai` and its response, which resolved to IP address `160.79.104.10`. I then confirmed this exact IP appeared in a TCP handshake shortly after, proving the full chain: typing a domain name triggers a DNS lookup, which returns an IP, which is then used to establish the actual connection.

**Mini Investigation (Module 3 Capstone):** I opened tradingview.com, which triggered my computer to ask my local DNS server for the address of `news-mediator.tradingview.com`. The DNS server responded with several possible IP addresses, and I isolated one: `54.230.201.108`. I then found the TCP handshake (SYN, then SYN-ACK) between my device and that IP over port 443, confirming a secure connection was established to load that part of the site.
