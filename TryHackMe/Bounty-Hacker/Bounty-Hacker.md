# bounty-hacker-writeup
OVERVIEW
This project documents the full penetration testing process of the Bounty Hacker room on Tryhackme. The objective was to simulate a real-world attack scenario involving reconnaissance, enumeration, exploitation, and privilege escalation.

OBJECTIVES  
- Perform network scanning and enumeration  
- Identify vulnerabilities in exposed services  
- Gain initial access  
- Escalate privileges to root  
- Capture all flags

TOOLS USED
- Nmap (Port Scanning & Service Detection)  
- FTP (File Access)  
- Gobuster (Directory Bruteforce)  
- Hydra (Brute Force Attack)  
- Netcat (Reverse Shell)  
- GTFOBins (Privilege Escalation)  
- Linux Enumeration Commands

TARGET INFORMATION
  Target IP: 
  Machine Name: Bounty Hacker  
  Platform: TryHackMe

1.RECONNAISSANCE AND SCANNING

Command used: nmap -sC -sV 10.49.xxx

![Nmap Scan](screenshots/nmap%20scan.png)

Results
    - Port 21 → FTP
    - Port 22 → SSH
    - Port 80 → HTTP
Analysis
    - FTP may allow anonymous login
    - Web server might contain hidden directories
    - SSH could be used for remote access after credentials are found

2.ENUMERATION

During the enumeration phase, an FTP service was discovered running on port 21
The FTP server allowed anonymous authentication:

command used: ftp 10.49.xxx
username: anonymous
password: anonymous

![FTP Access](screenshots/ftp%20access.png)

locks.txt
- Contains multiple potential passwords
- Acts as a **password wordlist**
Identified user name: lin

3.BRUTEFORCE ATTACK

Command used: hydra -l lin -P locks.txt ssh://10.49.xxx
Hydra, attack the **SSH service** on this target

![Hydra Bruteforce](screenshots/hydra%20brute%20force.png)

Credentials found
      Username: lin  
     Password: RedDr4gonSynd1cat3

4.SHELL ACCESS
Command used: ssh lin@10.49.159.xx

![SSH Access](screenshots/access%20via%20ssh%20.png)

successful login to lin account

![User Flag](screenshots/user%20flag.png)

5.PRIVILEGE ESCALATION
The command below was executed to identify binaries that could be run with elevated privileges:

![Root Permission](screenshots/root%20permission.png)

This indicates that the user **lin** is allowed to execute the `tar` binary with root privileges.
GTFOBins
    GTFOBins provides documented techniques for abusing Unix binaries to escalate privileges.
    The `tar` binary supports command execution through checkpoint actions, making it exploitable.
The following command was used to spawn a root shell:
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh

![Root Flag](screenshots/root%20flag.png)

successful login as root

![Flag Captured](screenshots/flag%20captured.png)

Conclusion

The **Bounty Hacker** machine provided a practical demonstration of a real-world penetration testing workflow, starting from initial reconnaissance to full system compromise.
During the engagement, I successfully:

- Performed **network scanning and enumeration** using Nmap to identify open services.
- Discovered valid credentials through **brute-force techniques (Hydra)**.
- Gained initial access via **SSH authentication**.
- Conducted **privilege escalation** by leveraging misconfigured binaries and referencing GTFOBins.
- Achieved full system compromise and captured both **user and root flags**.
    
This lab reinforced the importance of:

- Proper **credential management** and avoiding weak passwords.
- Securing services like SSH against brute-force attacks.
- Regular auditing of **SUID binaries and system permissions**.

Recommendations
- Enforce strong password policies
- Disable unnecessary services    
- Monitor login attempts (fail2ban)
- Restrict SUID permissions



