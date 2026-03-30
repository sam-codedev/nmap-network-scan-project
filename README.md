# Local Network Scan and Service Risk Analysis using Nmap

Summary

This report explains a network scan on the local machine (127.0.0.1). The goal was to find open ports, active services, and possible security problems.

The scan found one open port (631), which is used by the CUPS service. This service has some known vulnerabilities. However, because it can only be reached from the local computer, the overall risk is lower.

## Tools Used

- **Nmap** – the main tool for scanning networks, detecting open ports, and identifying services.  
- **Linux Terminal** – used to run Nmap commands and view the scan results directly.  
- **Web Browser** – used to research services and check for known vulnerabilities.  

## Key Activities

During the network scan, the following main activities were carried out:

1. **TCP Port Scanning**  
   Checked the local machine to see which TCP ports were open and listening.

2. **Service Version Detection**  
   Identified the versions of the services running on the open ports.

3. **Vulnerability Identification**  
   Used Nmap Scripting Engine (NSE) scripts to look for known weaknesses in the services.

4. **Service Exposure Verification**  
   Confirmed whether the detected services were accessible only locally or from outside.

5. **Risk Analysis**  
   Reviewed the findings to understand the level of risk and possible impact.

   ## Key Findings

During the scan, the following results were observed:

1. **Open Port Detected**  
   Port **631/tcp** was found to be open on the local machine.

2. **Service Identified**  
   The open port is running the **CUPS printing system** service.

3. **Vulnerabilities Found**  
   Known security issues were detected, including references such as **CVE‑2024‑47850**.

4. **Service Accessibility**  
   The service is only reachable from the local host (**127.0.0.1**) and is not exposed to external networks.

## Risk Assessment

The overall risk level is considered **Medium**.

- A vulnerable service (CUPS printing system) is running on the local machine.  
- This service has known security issues that could be exploited if exposed.  
- However, the service is only accessible from the local host (**127.0.0.1**) and is not open to external networks.  
- Because of this, the immediate risk is reduced, but updates and monitoring are still important.

## Recommendations

To reduce the risks found during the scan, the following actions are advised:

1. **Update the Service**  
   Make sure the CUPS printing system is upgraded to the latest version so that known security issues are fixed.

2. **Disable Unused Services**  
   Turn off any services that are not needed. This lowers the number of possible entry points for attackers.

3. **Apply Firewall Restrictions**  
   Use firewall rules to control access to the service. Allow only trusted connections and block unnecessary traffic.

## Installing Nmap
   ![image alt](https://github.com/sam-codedev/nmap-network-scan-project/blob/4e94576c55dcd18384effee77a28ccb5e28b6d73/Nmap-ver.jpg)

   It shows the process of installing **Nmap** on a Linux system.

1. At first, the user tried to run the command `nmap`.  
   The system replied that the command was not found, which means Nmap was not installed yet.

2. The terminal suggested two ways to install Nmap:  
   - `sudo snap install nmap` (version 7.95)  
   - `sudo apt install nmap` (an older version available in Ubuntu repositories)

3. The user chose the **snap method** and typed:

    - `sudo snap install nmap` 

After entering the password, the installation was successful.
The terminal confirmed that Nmap version 7.95 was installed from the Snap store.

## Service Version Scan
   ![image alt](https://github.com/sam-codedev/nmap-network-scan-project/blob/55cd340bde5e004b782b706f9908d0e82d9d98de/nmap-sV.jpg)

   This shows the result of running the command:

    nmap -sV 127.0.0.1p

### Which Happened
- The scan was done on **127.0.0.1** (localhost).  
- Nmap checked all TCP ports and found that most were closed.  
- One port, **631/tcp**, was open.  
- The service running on this port was identified as **CUPS 2.4** (Common Unix Printing System).

### Why It Matters
- Detecting service versions helps us know exactly what software is running.  
- With this information, we can check if the service has known vulnerabilities.  
- In this case, the printing service is only available locally, which lowers the risk.

## Vulnerability Scan
   ![image alt](https://github.com/sam-codedev/nmap-network-scan-project/blob/85432c11043f6da3f35a1f76333236fb42e014d2/vuln-result.jpg)

   This shows the result of running the command:

    nmap -sV -p 631 --script=vuln 127.0.0.1

### Which Happened

-The scan focused on port 631/tcp, which was already detected as open.
-Nmap confirmed that the service running on this port is CUPS 2.4 (Common Unix Printing System).
-The vulnerability scripts reported several known issues and possible exploits linked to this service.
-Some results also suggested possible admin directories that could be sensitive if exposed.

### Why It Matters

-Vulnerability scans help us check if the detected service has security problems.
-Knowing the CVEs and exploit references allows us to understand the severity of the risk.
-In this case, the service is only accessible locally, which reduces the chance of external attacks, but the vulnerabilities are still important to fix.
   
## CUPS Web Interface
   ![image alt](https://github.com/sam-codedev/nmap-network-scan-project/blob/ddcf787ac5d01a23f0f8e571604fcbb89cadb1cb/browser-page.jpg)

   This shows the local web page for **CUPS 2.4.1**, accessed at:
   
      http://127.0.0.1:631 (127.0.0.1 in Bing)

### Which Happened
- After scanning the system, the service on port **631/tcp** was confirmed to be CUPS.  
- Opening the address in a browser displayed the CUPS web interface.  
- The page provides sections for **Users**, **Administrators**, and **Developers**, with links to documentation and management options.

### Why It Matters
- The web interface proves that the service is active and reachable on the local machine.  
- It shows how administrators can manage printers, policies, and configurations.  
- If this page were exposed to external networks, it could be a security risk, so keeping it local is safer.

## Port Check and Service Exposure
   ![image alt](https://github.com/sam-codedev/nmap-network-scan-project/blob/aa1eaf9e43aa59fe1dd17ae44f6200465d95246d/tulnp.jpg)

   This shows the result of checking open ports and verifying service exposure.

### Which Happened
- The Nmap scan listed several possible folders and admin paths that could exist on the server.  
- After the scan, the command `ss -tulnp | grep 631` was used to check if port **631/tcp** was listening.  
- The output confirmed that the port is open and bound to **127.0.0.1** and **[::1]**, which means it is only accessible locally.

### Why It Matters
- Checking with `ss` helps confirm that the service is not exposed to external networks.  
- Even though vulnerabilities were detected earlier, limiting access to localhost reduces the risk of outside attacks.  
- This step shows how to verify whether a service is reachable from outside or only from the local machine.

## Disclaimer

This project is for **learning and practice purposes only**.  
All scans were performed on the local machine using the IP address **127.0.0.1 (localhost)**.  

- No external or public systems were scanned.  
- The results only show services running on the local computer.  
- This project does not expose sensitive information.  

It is safe to make this repository public because the IPs used are standard local addresses and do not reveal private or external networks.
