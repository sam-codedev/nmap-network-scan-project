# Local Network Scan and Service Risk Analysis using Nmap

Summary

This report explains a network scan on the local machine (127.0.0.1). The goal was to find open ports, active services, and possible security problems.

The scan found one open port (631), which is used by the CUPS service. This service has some known vulnerabilities. However, because it can only be reached from the local computer, the overall risk is lower.

## Tools Used

- **Nmap** – the main tool for scanning networks, detecting open ports, and identifying services.  
- **Linux Terminal** – used to run Nmap commands and view the scan results directly.  
- **Web Browser** – used to research services and check for known vulnerabilities.  
