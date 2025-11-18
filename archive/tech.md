As a technical cybersecurity analyst with 10 years of experience, the cyber-heist perpetrated against Bangladesh Bank (BB) in 2016 reveals critical failures across multiple technical domains, including endpoint security, network architecture, intrusion detection, and critical system hardening.
The attack was characterized as a wide-ranging, multi-year conspiracy involving reconnaissance, intrusion, data theft, and financial fraud
.
Here is an analysis of the primary technical flaws exploited at Bangladesh Bank and proposed superior technical approaches to mitigate similar threats.
--------------------------------------------------------------------------------
Technical Flaws Identified at Bangladesh Bank
The successful compromise and execution of fraudulent SWIFT transactions demonstrate several key security weaknesses:
1. Weak Endpoint Security and Triage Capability
The initial breach relied on basic, yet effective, initial access vectors:
• Successful Spear-Phishing Delivery: The subjects used tailored and personalized spear-phishing emails containing malicious links to gain unauthorized access to the network
. These emails often disguised malicious links as résumés or cover letters. The fact that targeted employees successfully downloaded the malware payload (Resum.zip) indicates that the bank’s email filtering/gateway security and user defenses failed to block the malicious content or prevent user interaction
.
• Malware Execution and Evasion: The attackers used sophisticated malware families, including NESTEGG (a memory-resident backdoor) [170.b, 250] and MACKTRUCK variants [170.c]. NESTEGG was designed to run in the computer’s memory without residing on the hard drive, making it inherently difficult for traditional anti-virus (AV) software to detect [170.b].
2. Lack of Network Segmentation and Privilege Separation
The post-compromise activity highlights inadequate controls between low-trust areas (employee workstations, email systems) and high-value critical systems:
• Lateral Movement to SWIFT Systems: After infecting an initial endpoint, the attackers successfully moved through the bank’s internal network to access the computer terminals interfacing with the SWIFT communication system (SWIFTLIVE)
. This lack of effective segmentation allowed a compromise originating on a generic employee machine to rapidly affect the most critical financial transaction system.
• Improper Privilege Management: The attackers were able to gain sufficient privileges to impersonate authorized bank employees and craft/send fraudulent but authenticated SWIFT messages
. This indicates that access controls on the SWIFT terminals themselves were likely restricted primarily to authentication mechanisms that the malware could bypass or credentials that the attackers could steal, rather than robust, multi-layered controls.
3. Failure in Intrusion Detection and Transaction Monitoring
The mechanisms designed to detect covert communications and unauthorized system modifications were bypassed:
• FakeTLS Protocol Bypass: The subjects utilized a custom communication protocol known as FakeTLS (Transport Layer Security) in malware like MACKTRUCK and Contopee [164.b.i, 170.c, 231, 232]. This protocol mimics authentic encrypted TLS traffic [164.b.i] but uses a different encryption method, allowing the hackers to carry on communications without triggering security alerts in systems designed to ignore encrypted traffic (assuming it is benign/standard)
.
• Integrity of Audit Trails Compromised: The subjects deployed malware (evtdiag.exe) specifically to interfere with the bank's transaction audit processes. This malware was configured to access the database storing SWIFT message records and delete the specific messages that instructed the fraudulent transactions
. Additionally, malware was employed to interfere with the generation of document confirmations (PDFs or hard copies)
. This points to a fundamental flaw in securing the integrity and redundancy of critical financial logs.
Proposed Better Technical Approaches
Based on these exploited flaws, the following technical controls and architectural changes should be prioritized:
1. Robust Endpoint and Gateway Protection (Preventative Layer)
• Enhanced Email Gateway Sandboxing and Filtering: Implement advanced sandboxing capabilities at the email gateway to dynamically execute and analyze file attachments (like Resum.zip) and embedded links before they reach the endpoint, specifically looking for attempts to communicate using non-standard or custom protocols like FakeTLS
.
• Application Whitelisting and Strict Execution Policies: On all systems, particularly privileged or critical terminals, enforce application whitelisting. This prevents the execution of any unauthorized program, including unknown droppers (like the one used for NESTEGG) or executables masquerading as benign files (e.g., hkcmd.exe or Flash video files) [172, 170.b, 171].
• Deployment of Modern EDR Tools: Replace traditional anti-virus with Endpoint Detection and Response (EDR) solutions. EDR tools are vital for detecting advanced threats like NESTEGG by continuously monitoring system memory for malicious code injection, process injection, and anomalous behavior, such as a process making an unusual external network call or attempting to modify system files [170.b].
2. Zero Trust Architecture and Critical System Segmentation
• Mandatory Micro-Segmentation for Critical Systems: The SWIFT Alliance Access application servers must be completely isolated, or micro-segmented, from the general corporate network. Communication to and from these servers must be limited strictly to necessary ports and protocols, defined by a Zero Trust model ("never trust, always verify")
.
• Restricted Administrative Access Path (Jump Servers): Access to critical systems like the SWIFT terminals should only be permitted through dedicated, highly secured Jump Servers or Bastion Hosts. These servers must enforce strong MFA, privileged access management (PAM), and rigorous session monitoring, ensuring that a compromised employee workstation cannot directly bridge to the SWIFT environment.
3. Deep Traffic Inspection and Protocol Analysis (Detection Layer)
• Network Detection and Response (NDR) for Protocol Anomaly: Deploy Network Detection and Response tools with deep packet inspection capabilities. These tools should be configured to analyze traffic, even on standard encrypted ports (like TCP 443), for non-standard or proprietary cryptographic handshakes and data structures (i.e., identifying the FakeTLS signature even if firewalls are instructed to ignore legitimate TLS traffic)
.
• Baseline Critical Network Activity: Establish a comprehensive baseline of expected network traffic and timing for SWIFT systems. Any deviation—such as communication with a dynamic DNS (DDNS) domain or a sudden increase in data transfer volumes (exfiltration attempts)—should trigger an immediate, high-priority alert
.
4. Immutable Auditing and Transaction Integrity (Resilience Layer)
• Write-Once, Read-Many (WORM) Logging: All logs pertaining to SWIFT transactions, system modification attempts (e.g., login failures, firewall changes), and malware activity must be recorded immediately to an immutable log server (or SIEM) located off-network or in a secured, segmented network space
. This prevents the attacker’s "secure delete" function (evtdiag.exe) from successfully erasing the audit trail, ensuring forensic artifacts remain even if the local host is destroyed
.
• Mandatory Multi-Factor Transaction Verification: Implement an architectural control requiring multi-party authorization and out-of-band verification for SWIFT message creation and release. This verification should involve confirmation via systems physically and logically separated from the primary network interface, thus thwarting attempts at impersonation through terminal access alone
.
By implementing robust controls in these four areas, Bangladesh Bank (or any similar financial institution) could significantly reduce the attack surface, detect unauthorized activities in real-time, and ensure that even if an initial compromise occurs, the attacker is unable to pivot to critical systems or tamper with the forensic evidence required for effective incident response.
--------------------------------------------------------------------------------
Analogy: Consider the bank's network infrastructure not as a single walled building, but as a series of nested vaults. The flaw at Bangladesh Bank was treating all interior walls as equally penetrable, allowing the attacker who picked the front-door lock (spear-phishing) to walk freely to the innermost vault (the SWIFT system). A better approach mandates that the inner vault is sealed, requires separate, complex keys (MFA) to enter, and has hidden sensors (NDR/EDR) that detect peculiar movements (FakeTLS) even before a human monitor (the banking staff) notices the transaction records are being physically shredded (secure delete).