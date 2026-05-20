# root-me-tryhackme-writeup

1. LAB INFORMATION
- **Room:** RootMe
    
- **Platform:** TryHackMe
    
- **Goal:** Gain initial access, escalate privileges, and capture both flags.
    
- **Environment:** Kali Linux attacking machine against the deployed target machine.

2. METHODOLOGY OVERVIEW
- Reconnaissance
    
- Enumeration
    
- Initial Access
    
- Shell Stabilization
    
- Privilege Escalation
    
- Flag Collection
    
- Lessons Learned
3. RECONNAISSANCE
Identify open ports, services, and potential entry points.
command used: nmap -Pn -A  IP 

![Nmap scan](screenshots/nmap-scan.png)



The machine exposes
22/tcp open ssh
80/tcp open HTTP

4. WEB ENUMERATION
Discover hidden directories and web functionality.
Command used:  gobuster dir --wordlist=/usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://IP

![Gobuster Scan](screenshots/gobuster-scan.png)


/panel is a login or a control panel which is also a hidden directory displayed by gobuster tool

5. INITIAL ACCESS

![Target Address](screenshots/target-address.png)

The ip shows the vulnerable website
![Upload Functionality](screenshots/upload-functionality.png)

The upload panel has an upload functionality where we can upload a shell for command line access
An upload of a shell.php file was done to gain a reverse shell 

![Payload Configuration](screenshots/payload-configuration.png)

During payload configuration i was able to change to my attacker ip address to initiate a netcat listener later on port 1234

![Upload Shell](screenshots/upload-shell.png)

 After uploading the reverse shell the website declined a php but we can introduce new file formats like bak, php5 using burpsuite
 
![Burp Requests](screenshots/capturing-requests-burpsuit.png)

 using burp proxy capture the request through intercept and send to intruder in burpsuit
![Payload Upload](screenshots/payload-upload.png)

select php in sniper attack and add different file types 

![Payloads](screenshots/payloads.png)

we have successfully uploaded our reverse shells to the target 

![Payload Uploaded](screenshots/payload-uploaded.png)

6. SHELL STABILIZATION
Set a netcat listener on port 1234 
command used: nc -nlvp 1234

![Netcat listener](screenshots/netcat-listener.png)

 Now we have access as a normal user
 command used: find / -type f -name user.txt 2> /dev/null which means everything else is redirected to null
 
![Flag Captured](screenshots/flag-captured.png)
 
 thats our flag
 
7. PRIVILEGE ESCALATION
Lets try to access as root user
command used: find / -type f -user root -perm -u=s 2> /dev/null
Finds files owned by root that have SUID permission
when Set User Id files are run they run as root user

![Python Privilege Escalation](screenshots/python-privilege-escalation.png)

we can use GTFO bins to get the program python to escalate privilages
command used: python2.7 -c 'import os; os.setuid(0); os.system("/bin/sh")'
"/bin/sh" gives a shell

![Privilege Escalation](screenshots/privilege-escalation.png)
we are now root user
command used: find / -type f -name root.txt 2> /dev/null

![Root Flag Captured](screenshots/root-flag-captured.png)

OVERVIEW

Conclusion

This lab demonstrated a full attack chain from initial enumeration to privilege escalation. Starting with reconnaissance, I identified accessible services and used directory enumeration to discover a vulnerable file upload functionality. By bypassing file upload restrictions, I successfully deployed a PHP reverse shell and gained remote access to the target system.

During post-exploitation, I performed privilege escalation by enumerating SUID binaries and identified a misconfigured Python binary. Using this, I was able to escalate privileges and obtain root access.

This exercise reinforced the importance of:

- Proper input validation on file uploads
    
- Secure configuration of system binaries
    
- Thorough enumeration during post-exploitation
    

Overall, the lab provided practical experience in web exploitation, reverse shells, and privilege escalation techniques, which are critical skills in real-world penetration testing.

