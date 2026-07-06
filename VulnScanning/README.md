## Goal
Run comprehensive vulnerability scans against a deliberately vulnerable staging server to identify outdated software, open ports, and misconfigurations.

## Environment
- Target: Metasploitable2 (intentionally vulnerable VM, run in an isolated Host-only VirtualBox network on my own machine)
- Scanner: Nmap 7.99

## Tools Used
- VirtualBox
- Nmap (-sV -sC -p-)

## Process
1. Deployed Metasploitable2 in VirtualBox on a Host-only network (isolated from internet)
2. Identified target IP via `ifconfig`
3. Ran a full port scan with service/version detection: `nmap -sV -sC -p- <target-ip> -oN nmap_scan_results.txt`
4. Cross-referenced discovered service versions against known CVEs
5. Built a prioritized patch list ranked by CVSS severity

## Key Findings
- 16 vulnerabilities identified, 7 rated Critical (CVSS 9.0+)
- Most severe: a literal open root shell (port 1524), backdoored vsftpd (port 21), and unauthenticated Java RMI (port 1099) — all allowing remote code execution without credentials

## Deliverables
- [nmap_scan_results.txt](nmap_scan_results.txt) — full scan output
- [prioritized_patch_list.xlsx](prioritized_patch_list.xlsx) — CVSS-ranked vulnerability list with fixes

## Disclaimer
All scanning was performed against a deliberately vulnerable VM in an isolated lab environment on my own machine — no external or unauthorized systems were targeted.
