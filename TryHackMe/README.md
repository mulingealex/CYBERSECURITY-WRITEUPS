# TryHackMe — Penetration Testing Write-ups

[![TryHackMe](https://img.shields.io/badge/Platform-TryHackMe-212C42?style=flat)](https://tryhackme.com)
[![License](https://img.shields.io/badge/License-Educational-lightgrey)](.)

Personal, portfolio-ready walkthroughs for [TryHackMe](https://tryhackme.com) rooms. Each project documents a full attack lifecycle—**reconnaissance**, **enumeration**, **exploitation**, **privilege escalation**, and **key takeaways**—with screenshots, command references, and defensive recommendations.

These labs support applications for **cybersecurity internships**, **SOC analyst** roles, and **junior penetration testing** positions.

---

## Rooms Completed

| Room | Difficulty | Focus Areas | Write-up |
|------|------------|-------------|----------|
| **Bounty Hacker** | Easy | Nmap, FTP, Hydra, SSH, sudo/GTFOBins | [Bounty-Hacker/README.md](Bounty-Hacker/README.md) |
| **Kenobi** | Easy | SMB, NFS, ProFTPD, SSH keys, SUID PATH hijack | [Kenobi/README.md](Kenobi/README.md) |
| **RootMe** | Easy | Gobuster, upload bypass, Burp Suite, reverse shell, SUID Python | [RootMe/README.md](RootMe/README.md) |

---

## Skills Matrix (Across Labs)

| Skill | Bounty Hacker | Kenobi | RootMe |
|-------|:-------------:|:------:|:------:|
| Network reconnaissance (Nmap) | ✓ | ✓ | ✓ |
| Service / share enumeration | ✓ | ✓ | ✓ |
| Credential attacks | ✓ | — | — |
| Web enumeration & exploitation | — | — | ✓ |
| Linux privilege escalation | ✓ | ✓ | ✓ |
| Remediation & defensive guidance | ✓ | ✓ | ✓ |

---

## Repository Layout

```
TryHackMe/
├── Bounty-Hacker/
│   ├── README.md
│   └── screenshots/
├── Kenobi/
│   ├── README.md
│   └── screenshots/
└── RootMe/
    ├── README.md
    └── screenshots/
```

Each room folder contains a standalone **README** (GitHub renders it automatically when browsing the directory) and a `screenshots/` directory with evidence images referenced via relative paths.

---

## Tools Referenced

`Nmap` · `Gobuster` · `Hydra` · `FTP` · `smbclient` · `showmount` · `Burp Suite` · `Netcat` · `SSH` · `GTFOBins` · Linux enumeration (`find`, `sudo`, `grep`, `mount`)

---

*All write-ups are for authorized, educational lab environments only.*
