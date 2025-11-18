# Bangladesh Bank Cyber-Heist: Technical Flaws and Mitigation Strategies

## Executive Summary

The successful cyber-heist against Bangladesh Bank (BB) in 2016 exposed critical technical failures across three main domains: Weak Endpoint and Gateway Protection, Insufficient Network Segmentation and Privilege Control, and Failure in Detection and Audit Integrity. The perpetrators utilized a wide-ranging, multi-year conspiracy involving reconnaissance, intrusion, data theft, and financial fraud.

Drawing on the technical details of the intrusion, this document provides an analysis of the specific technical flaws the bank demonstrated and proposes superior technical approaches to mitigate similar threats.

---

## Technical Flaws Identified at Bangladesh Bank

### 1. Weak Endpoint Security and Triage Capability

The initial network compromise highlights a lack of preventative layers and detection capability at the network edge and on user machines.

| Technical Flaw/Lack | Supporting Detail |
|---------------------|-------------------|
| **Failure of User and Gateway Defenses** | The subjects used tailored and personalized spear-phishing emails containing malicious links, often disguised as résumés or cover letters (`Resum.zip`), to gain unauthorized access. The fact that targeted employees successfully downloaded the malicious payload indicates the bank's email filtering/gateway security and user defenses failed to block the content or prevent user interaction. |
| **Inadequate Anti-Virus (AV) Capability** | The attackers deployed sophisticated malware designed for evasion, including the NESTEGG backdoor [170.b, 250, 622]. NESTEGG is a memory-resident backdoor that runs without residing on the hard drive, making it inherently difficult for traditional anti-virus (AV) software to detect [170.b, 622]. |

### 2. Lack of Network Segmentation and Privilege Separation

The ability of the attackers to move from a standard workstation to the most critical systems demonstrates a critical architectural weakness.

| Technical Flaw/Lack | Supporting Detail |
|---------------------|-------------------|
| **Inadequate Network Segmentation** | After infecting an initial endpoint, the attackers successfully moved laterally through the internal network to access the computer terminals interfacing with the SWIFT communication system (SWIFTLIVE) [2, 7, 8, 164.c, 623]. This lack of effective segmentation allowed a compromise originating on a low-trust employee machine to rapidly affect the most critical financial transaction system. |
| **Improper Privilege Management** | The attackers were able to gain sufficient privileges to impersonate authorized bank employees and craft/send fraudulent but authenticated SWIFT messages. Access controls on the SWIFT terminals were likely restricted primarily to authentication mechanisms that the malware could bypass or credentials that the attackers could steal, rather than robust, multi-layered controls. |

### 3. Failure in Intrusion Detection and Transaction Monitoring

The bank lacked controls to detect covert communication channels and ensure the permanence of its audit records.

| Technical Flaw/Lack | Supporting Detail |
|---------------------|-------------------|
| **Failure to Detect Custom Protocols** | The subjects utilized a custom communication protocol known as FakeTLS in malware variants (like MACKTRUCK and Contopee) [164.b.i, 170.c, 231, 232, 624]. This protocol mimics authentic encrypted TLS traffic but uses a different encryption method [164.b.i], allowing the hackers to carry on communications without triggering security alerts in systems designed to ignore encrypted traffic. |
| **Compromised Audit Trail Integrity** | The subjects deployed malware (`evtdiag.exe`) specifically to interfere with transaction audit processes. This malware was configured to access the database storing SWIFT message records and delete the specific messages that instructed the fraudulent transactions. Malware was also used to interfere with the generation of document confirmations (PDFs or hard copies). |

---

## Proposed Superior Technical Approaches

To address these vulnerabilities, Bangladesh Bank should prioritize implementing security controls across preventative, detection, and resilience layers, moving toward a Zero Trust architectural model.

### 1. Robust Endpoint and Gateway Protection (Preventative Layer)

The bank needs to enhance its defenses at the entry points and on individual machines.

- **Enhanced Email Gateway Sandboxing and Filtering**: Implement advanced sandboxing at the email gateway. This dynamically executes and analyzes file attachments (`Resum.zip`) and embedded links before they reach the endpoint, specifically searching for attempts to communicate using non-standard or custom protocols like FakeTLS.

- **Application Whitelisting and Strict Execution Policies**: Enforce application whitelisting on all systems, especially privileged or critical terminals. This prevents the execution of unauthorized programs, including unknown malware droppers (like the one used for NESTEGG) or executables masquerading as legitimate files (e.g., `hkcmd.exe`) [172, 170.b, 171, 625].

- **Deployment of Modern EDR Tools**: Replace traditional anti-virus with Endpoint Detection and Response (EDR) solutions. EDR tools are vital for detecting advanced threats like NESTEGG by continuously monitoring system memory for malicious code injection and anomalous behavior, necessary for catching malware that avoids the hard drive [170.b, 625].

### 2. Zero Trust Architecture and Critical System Segmentation

Critical infrastructure must be isolated to prevent lateral movement, even if an internal workstation is compromised.

- **Mandatory Micro-Segmentation for Critical Systems**: SWIFT Alliance Access application servers must be completely isolated, or micro-segmented, from the general corporate network. Communication must be strictly limited to necessary ports and protocols, defined by a Zero Trust model ("never trust, always verify").

- **Restricted Administrative Access Path (Jump Servers)**: Access to critical systems, such as SWIFT terminals, should only be permitted through dedicated, highly secured Jump Servers or Bastion Hosts. These servers must enforce strong Multi-Factor Authentication (MFA), privileged access management (PAM), and rigorous session monitoring to ensure a compromised employee workstation cannot directly bridge to the SWIFT environment.

### 3. Deep Traffic Inspection and Protocol Analysis (Detection Layer)

The network must actively hunt for covert channels and anomalous behavior.

- **Network Detection and Response (NDR) for Protocol Anomaly**: Deploy NDR tools with deep packet inspection capabilities. These should be configured to analyze traffic, even on standard encrypted ports (like TCP 443), for non-standard or proprietary cryptographic handshakes (i.e., identifying the FakeTLS signature).

- **Baseline Critical Network Activity**: Establish a comprehensive baseline of expected network traffic and timing for all SWIFT systems. Any deviation—such as communication with a dynamic DNS (DDNS) domain or a sudden increase in data exfiltration—should trigger an immediate, high-priority alert.

### 4. Immutable Auditing and Transaction Integrity (Resilience Layer)

The bank needs fail-safes to ensure forensic data and transaction authorization cannot be compromised.

- **Write-Once, Read-Many (WORM) Logging**: All logs relating to SWIFT transactions, system modification attempts (e.g., login failures), and malware activity must be recorded immediately to an immutable log server (or SIEM) located in a secured, segmented network space. This prevents the attacker's "secure delete" function (used by `evtdiag.exe`) from successfully erasing the audit trail, guaranteeing forensic artifacts remain even if the local host is destroyed.

- **Mandatory Multi-Factor Transaction Verification**: Implement an architectural control requiring multi-party authorization and out-of-band verification for SWIFT message creation and release. This confirmation must utilize systems physically and logically separated from the primary network interface, thus thwarting attempts at impersonation achieved solely through terminal access.

---

## Conclusion

The breach of Bangladesh Bank highlights a reliance on perimeter defenses that failed under a sophisticated, persistent threat. The suggested shift involves adopting a **Zero Trust model** where detection and verification layers are woven throughout the architecture, ensuring that even if one component fails (like a compromised employee endpoint), critical systems (like the SWIFT terminals and audit logs) remain resilient and isolated.

---

## Key Recommendations Summary

1. **Prevention**: Deploy EDR, email sandboxing, and application whitelisting
2. **Segmentation**: Implement micro-segmentation and jump servers for critical systems
3. **Detection**: Use NDR tools with deep packet inspection to identify anomalous protocols
4. **Resilience**: Ensure immutable audit logs and multi-factor transaction verification
5. **Architecture**: Adopt Zero Trust principles throughout the infrastructure
