# parrot-audit
This project demonstrates how to perform a **basic network and system audit** using open-source tools in **Parrot OS**. 
 1. Objective
This project demonstrates how to perform a **basic network and system audit** using open-source tools in **Parrot OS**.  
The goal was to:
- Scan a **Windows 11** host on the local network.
- Audit the **Parrot OS** workstation itself for system hardening.
- Document findings and recommendations as a sample cybersecurity report.

---

## ⚙️ 2. Tools Used
| Tool | Purpose |
|------|----------|
| **Nmap** | Network discovery, port scanning, OS and service detection |
| **Lynis** | Host-based system auditing and configuration analysis |
| **Parrot OS** | Linux distribution designed for ethical hacking and forensics |

---

## 🧱 3. Setup
Project directory structure:

~/projects/parrot-audit/ ├── scans/ │ ├── nmap_192.168.56.1_advanced.txt │ └── lynis_parrot_audit.txt └── README.md

---

## 🧭 4. Procedure

### 🔹 Step 1: Network Scan (External Audit)
**Target:** Windows 11 host at `192.168.56.1`

**Command:**
```bash
sudo nmap -sS -A 192.168.56.1 -oN scans/nmap_192.168.56.1_advanced.txt

Purpose:
Identify open ports, running services, and the OS of the Windows 11 system.

Key Findings:

Port State Service Notes

22/tcp filtered ssh Blocked by Windows Firewall
23/tcp filtered telnet Disabled (default on Windows 11)
179/tcp filtered bgp Not in use
646/tcp open tcpwrapped Secure wrapper, closed quickly
OS Detection inconclusive – Firewall prevented fingerprinting


Interpretation:
Windows 11’s firewall effectively filtered most probes.
The “tcpwrapped” response suggests secure service handling or virtual network protection.


---

🔹 Step 2: System Audit (Internal Audit)

Target: Parrot OS (auditing machine)

Command:

sudo lynis audit system > scans/lynis_parrot_audit.txt

Purpose:
Evaluate Parrot OS security posture, configurations, and possible weaknesses.

Example Output Summary:

Hardening index : 72 [of 100]
Warning: No password policy found for users
Suggestion: Enable UFW firewall
Suggestion: Review system log rotation


---

📊 5. Analysis

Area Finding Recommendation

Network 4 ports filtered on Windows host Maintain Windows Firewall protection
OS Detection Obscured by filtering Temporarily allow ICMP for deeper scan
Parrot System Moderate hardening (72/100) Apply Lynis recommendations for improved security



---

🧾 6. Conclusion

This project demonstrated how to use Nmap and Lynis to perform entry-level cybersecurity audits:

The Windows 11 system is properly firewalled and resists basic scanning.

The Parrot OS system is secure but can be hardened further.


This workflow mirrors what professional penetration testers and system administrators do to assess and improve network and system security.


---

📎 7. Attachments

scans/nmap_192.168.56.1_advanced.txt – raw Nmap output

scans/lynis_parrot_audit.txt – Lynis audit report

screenshots/ – (Add your terminal screenshots here)



---

🚀 8. Future Work

Automate Nmap and Lynis runs using shell scripts.
