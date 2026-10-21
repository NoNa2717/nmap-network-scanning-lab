# Nmap Network Scanning Lab

A beginner cybersecurity lab documenting network discovery and service enumeration with **Nmap**, using a controlled virtual lab with **Kali Linux** and **Windows 10**.

> **Portfolio note:** This README is based on my lab notes. It describes the activities and observations documented in the original report. Add your own screenshots and exact command output before publishing; no scan results or IP addresses have been invented here.

## Project overview

The purpose of this lab was to practise identifying hosts, checking network connectivity, discovering open ports, and reviewing service information in a small lab network.

### Lab environment

- **Attacker / scanning machine:** Kali Linux
- **Target machines:** Windows 10
- **Web and database stack:** XAMPP, with Apache and MySQL services running
- **Network:** Lab machines connected to the same network

Only scan systems you own or have explicit permission to assess.

## Objectives

- Verify connectivity between Kali Linux and the Windows lab machines.
- Discover hosts and open ports with Nmap.
- Identify services associated with discovered ports.
- Practise HTTP/HTTPS and UDP scanning.
- Save scan results for review and documentation.
- Understand how service and version information can support defensive security assessments.

## Methodology

### 1. Verify network connectivity

I used `ping` from Kali Linux to test connectivity to the Windows lab machines. The ping test succeeded, confirming that the machines could communicate over the lab network.

Example command (replace the placeholder with your own lab target):

```bash
ping <TARGET_IP>
```

### 2. Discover hosts and scan TCP ports

I used Nmap to identify devices on the lab network and inspect open ports.

```bash
nmap <TARGET_IP>
```

For a lab subnet you control, host discovery can be performed with:

```bash
nmap -sn <YOUR_LAB_SUBNET>
```

Document the exact target range and command you used in your final report. Do not scan networks without permission.

### 3. Review discovered services

The lab notes recorded these observations:

| Port | Service noted | Interpretation |
|---|---|---|
| `80/tcp` | HTTP / Apache | A web service was available on the Windows lab machines. |
| `3306/tcp` | MySQL | A database service appeared to be listening. |
| `443/tcp` | HTTPS | The notes recorded this port as open during the HTTP/HTTPS scan. |

These are observations from this lab, not universal defaults or proof that a service is vulnerable. Confirm service details from the actual scan output.

### 4. Service and version detection

Nmap was used to identify operating-system information and the names/versions of services where possible. This information can help a security analyst determine what needs further validation.

Example command:

```bash
nmap -sV -O <TARGET_IP>
```

OS detection may require elevated privileges and may not always identify an operating system accurately. Service/version results should be treated as clues, not definitive proof.

### 5. HTTP/HTTPS port checks

I checked the HTTP and HTTPS ports. The lab notes record port `80` as open for Apache/HTTP and port `443` as open.

Example command:

```bash
nmap -p 80,443 <TARGET_IP>
```

An open port indicates that a service may be reachable; it does not by itself establish whether the service is configured securely.

### 6. UDP scanning

I also practised UDP scanning as part of the lab.

Example command (UDP scans can take time and may require elevated privileges):

```bash
sudo nmap -sU --top-ports 20 <TARGET_IP>
```

Record the actual command and output you used. UDP scan results can be inconclusive because many UDP services do not respond to probes.

### 7. Save scan results

Nmap can save output in a text format for later review:

```bash
nmap -oN reports/scan-results.txt <TARGET_IP>
```

For this public repository, remove private IPs, hostnames, usernames, and other information you do not want to publish. Only include output from your own authorised lab.

## Findings and security relevance

- **Host discovery and connectivity checks** help establish which lab systems are reachable.
- **Open-port discovery** provides an initial view of the network's exposed services.
- **Service/version identification** can help defenders prioritise further configuration and vulnerability checks.
- **HTTP, HTTPS, and database services** should be exposed only where needed and protected by suitable network controls.
- **UDP scanning** complements TCP checks because some services use UDP rather than TCP.

This lab was a discovery and enumeration exercise. It did **not**, based on the notes available, confirm exploitation or prove that any host was vulnerable.

## Evidence and screenshots

Add screenshots you captured from your own lab to the `screenshots/` folder, then update this section with the correct filenames.

Suggested evidence:
1. `01-lab-environment.png` — Kali Linux and Windows lab setup.
2. `02-ping-connectivity.png` — successful connectivity test.
3. `03-nmap-port-scan.png` — your Nmap port scan and output.
4. `04-service-version-scan.png` — service/version results, if captured.
5. `05-udp-scan.png` — UDP scan output, if captured.
6. `06-saved-results.png` — saved scan report, with sensitive details redacted.

No screenshots are included yet. Do not use screenshots that show systems you do not have permission to test.

## Skills demonstrated

- Nmap fundamentals
- Network connectivity troubleshooting
- Host discovery and port scanning
- Basic service enumeration
- Introductory TCP/UDP scanning
- Interpreting common web and database ports
- Security documentation and evidence handling

## What I learned

This lab helped me practise a structured initial network assessment: confirm connectivity, discover reachable hosts, inspect open ports, identify likely services, and document the results. I also learned that scan findings need context and validation; an open port alone does not mean a system is vulnerable.

## Possible next steps

- Add redacted screenshots and the exact commands/output from the lab.
- Verify service versions and compare them with vendor security advisories.
- Review whether the database service needs to be reachable from other machines.
- Repeat scans after making an authorised configuration change and compare the results.
- Add a short reflection on limitations, false positives, and defensive recommendations.

## Author

Cybersecurity student building practical skills in network security and security operations.

*This project was performed in a controlled lab environment for learning purposes.*
