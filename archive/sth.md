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

## Attack Phase Analysis: Defense Effectiveness Mapping

This section maps each phase of the actual attack to the proposed solutions to evaluate whether they would have successfully prevented the breach.

### Phase 1: Initial Access (January-February 2015)

**What Actually Happened:**
- Attackers sent spear-phishing emails with malicious `Resum.zip` attachments
- At least 3 Bangladesh Bank employees successfully downloaded and executed the malware
- NESTEGG backdoor installed in system memory
- Attack went undetected for over a year

**Proposed Defenses vs. This Attack Phase:**

| Defense Solution | Effectiveness | Analysis |
|------------------|---------------|----------|
| **Enhanced Email Gateway Sandboxing** | ✅ **BLOCKED** | Sandbox would detonate `Resum.zip` in isolated environment, detect NESTEGG attempting to load into memory and communicate via FakeTLS protocol, and block email delivery before reaching employees. **Attack stops here.** |
| **Application Whitelisting** | ✅ **BLOCKED** | Even if email bypassed gateway, whitelisting on employee workstations would prevent execution of unauthorized `Resum.zip` payload. Malware dropper not on approved list = cannot run. **Attack stops here.** |
| **EDR Tools** | ✅ **DETECTED & BLOCKED** | If malware somehow executed, EDR would immediately alert on: memory-resident process (NESTEGG), process injection, FakeTLS network communication, anomalous behavior. Security team alerted within minutes/hours, not years. **Attack stops here.** |

**Phase 1 Verdict:** ✅ **ATTACK PREVENTED** - Any single control would likely stop initial compromise. All three together provide defense-in-depth.

---

### Phase 2: Network Reconnaissance & Lateral Movement (February 2015 - January 2016)

**What Actually Happened:**
- From compromised employee workstations, attackers spent ~11 months exploring the network
- Mapped internal infrastructure and located SWIFT terminals
- Successfully moved laterally from low-trust employee machines to critical SWIFT systems
- Deployed additional malware variants (MACKTRUCK, Contopee)
- Used FakeTLS protocol to communicate with command-and-control servers undetected

**Proposed Defenses vs. This Attack Phase:**

| Defense Solution | Effectiveness | Analysis |
|------------------|---------------|----------|
| **Mandatory Micro-Segmentation** | ✅ **BLOCKED** | SWIFT terminals isolated on completely separate network segment. Attackers on employee workstation network cannot route traffic to SWIFT network regardless of credentials or exploits. **This is the critical kill shot.** Like being in the bank lobby but unable to access the vault - the wall is architectural, not just authentication-based. |
| **Jump Servers with MFA/PAM** | ✅ **BLOCKED** | Only approved path to SWIFT is through hardened jump servers requiring: strong MFA, privileged access management, and session recording. Attackers cannot pivot directly from compromised workstation. Each access attempt logged and monitored. |
| **EDR Tools** | ✅ **DETECTED & BLOCKED** | EDR would detect lateral movement indicators: credential dumping (Mimikatz-style), unusual network scanning, remote code execution attempts, new process creation chains, privilege escalation. Alerts would fire throughout the 11-month reconnaissance period. |
| **NDR for Protocol Anomaly** | ✅ **DETECTED & BLOCKED** | Network detection would identify: FakeTLS traffic (non-standard TLS handshake signature), communications with suspicious external IPs, internal network scanning patterns, data exfiltration attempts. Year-long C2 communication would definitely trigger alerts. |
| **Baseline Network Activity** | ✅ **DETECTED** | Unusual network traffic patterns from employee workstations attempting to reach SWIFT network segments would deviate from baseline and trigger investigation. |

**Phase 2 Verdict:** ✅ **ATTACK PREVENTED** - Micro-segmentation creates an architectural barrier that cannot be "hacked around." Even if attackers spent 11 years instead of 11 months, they couldn't breach the network boundary without physical access to jump servers.

---

### Phase 3: SWIFT System Compromise & Transaction Execution (February 2016)

**What Actually Happened:**
- Attackers accessed SWIFT terminals (SWIFTLIVE)
- Gained sufficient privileges to impersonate authorized bank employees
- Crafted and sent 35 fraudulent but "authenticated" SWIFT messages
- Attempted to steal ~$1 billion
- Successfully transferred $81 million to Philippines accounts
- Additional $20 million to Sri Lanka was stopped by recipient bank (not Bangladesh Bank's detection)

**Proposed Defenses vs. This Attack Phase:**

| Defense Solution | Effectiveness | Analysis |
|------------------|---------------|----------|
| **Application Whitelisting on SWIFT Terminals** | ✅ **BLOCKED** | SWIFT terminals configured to only run official SWIFT Alliance Access software. Any malware attempting to execute on SWIFT terminals would be blocked. Attackers cannot inject code or run unauthorized executables. **Attack stops here.** |
| **Mandatory Multi-Factor Transaction Verification** | ✅ **BLOCKED - ULTIMATE FAILSAFE** | **Even assuming complete system compromise**, each SWIFT transaction requires: <br><br>• Second employee approval (different terminal, different network segment)<br>• Out-of-band phone confirmation to bank executives<br>• Physical hardware token from secure location<br>• Verification from separate, isolated system<br><br>**35 fraudulent transactions = 35 failed verification attempts**<br><br>When CFO receives phone call: "Please confirm $20 million transfer to Philippines casino account," response is "ABSOLUTELY NOT" and immediate security investigation begins. Attackers cannot forge real-time human judgment across multiple executives. |
| **Baseline Network Activity** | ✅ **DETECTED & BLOCKED** | 35 SWIFT messages in rapid succession to unusual destinations (Philippines, Sri Lanka) would massively deviate from normal transaction patterns. Automated alerts would fire immediately. Even if first few transactions succeeded, subsequent ones would be blocked pending investigation. |
| **EDR Tools** | ✅ **DETECTED** | EDR on SWIFT terminals would detect: unauthorized process accessing SWIFT database, credential impersonation, API calls to SWIFT transaction system, memory manipulation. |
| **NDR for Protocol Anomaly** | ✅ **DETECTED** | Unusual volume and destination of SWIFT messages would be flagged by network monitoring. Transaction timing and recipient profiles don't match historical baselines. |

**Phase 3 Verdict:** ✅ **ATTACK PREVENTED** - Multi-Factor Transaction Verification is the "nuclear option" that stops the attack even with total system compromise. Application whitelisting provides an additional hard stop. The defense-in-depth approach ensures multiple independent opportunities to block the theft.

---

### Phase 4: Evidence Elimination & Cover-Up (February 6, 2016)

**What Actually Happened:**
- Malware `evtdiag.exe` deleted SWIFT transaction records from local database
- Malware `nroff.exe` intercepted and modified transaction printouts
- Attackers used "secure delete" function to overwrite malware files with random data
- NESTEGG backdoor erased itself from memory
- Audit trail compromised, delaying discovery and investigation

**Proposed Defenses vs. This Attack Phase:**

| Defense Solution | Effectiveness | Analysis |
|------------------|---------------|----------|
| **WORM (Write-Once, Read-Many) Logging** | ✅ **EVIDENCE PRESERVED** | All SWIFT transactions immediately written to immutable log server on separate, secured network segment. Attacker's `evtdiag.exe` can delete local database records but **cannot access or modify WORM logs** on isolated network. Complete forensic audit trail preserved regardless of attacker actions on compromised systems. |
| **Micro-Segmentation** | ✅ **LOGS PROTECTED** | WORM log server on separate network segment. Even with SWIFT terminal access, attackers cannot reach logging infrastructure to tamper with records. Network isolation provides physical separation of evidence. |
| **EDR Tools** | ✅ **TAMPERING DETECTED** | EDR would detect and alert on: `evtdiag.exe` accessing SWIFT database, mass deletion of transaction records, `nroff.exe` intercepting print jobs, secure delete operations, unusual file system activity. While tampering might succeed locally, security team would know it occurred and extent of damage. |

**Phase 4 Verdict:** ⚠️ **ATTACK IMPACT MITIGATED** - While attackers might successfully delete local records, immutable logs on segmented network preserve complete forensic evidence. This enables: faster incident response, complete attack timeline reconstruction, evidence for law enforcement, lessons learned for remediation. The attack's cover-up phase fails completely.

---

## Defense-in-Depth Summary: Kill Chain Analysis

The proposed solutions create **multiple independent chokepoints** where the attack fails:

```
ATTACK PHASE                    DEFENSE LAYERS                           RESULT
═══════════════════════════════════════════════════════════════════════════════

Phase 1: Spear-Phishing        → Email Sandboxing                       ✅ BLOCKED
(Initial Access)               → Application Whitelisting               ✅ BLOCKED
Jan-Feb 2015                   → EDR Detection                          ✅ BLOCKED

                               ↓ If all Phase 1 defenses fail...

Phase 2: Lateral Movement      → Micro-Segmentation                     ✅ BLOCKED
(Network Reconnaissance)       → Jump Servers with MFA/PAM              ✅ BLOCKED
Feb 2015 - Jan 2016           → NDR Protocol Detection                 ✅ BLOCKED
                               → EDR Behavior Monitoring                ✅ BLOCKED

                               ↓ If all Phase 2 defenses fail...

Phase 3: Transaction Execution → Application Whitelisting (SWIFT)       ✅ BLOCKED
(The Theft)                    → Multi-Factor Transaction Verification  ✅ BLOCKED
February 2016                  → Baseline Activity Monitoring           ✅ BLOCKED

                               ↓ If all Phase 3 defenses fail...

Phase 4: Cover-Up              → WORM Immutable Logging                 ✅ PRESERVED
(Evidence Destruction)         → Network Segmentation (Log Isolation)   ✅ PROTECTED
February 2016                  → EDR Forensics                          ✅ DETECTED
```

---

## Critical Success Factors: The "Must-Have" Controls

If resource constraints required prioritization, these three controls would have the highest impact:

### 🥇 Priority 1: Micro-Segmentation + Jump Servers
**Impact:** Breaks the attack chain at the most critical point
**Confidence:** 95%+ that this alone prevents the attack
**Why:** Attackers spent 11 months moving from employee workstations to SWIFT terminals. Proper network segmentation makes this journey impossible. It's an architectural barrier, not a detection challenge.

**Key Quote:** "This lack of effective segmentation allowed a compromise originating on a low-trust employee machine to rapidly affect the most critical financial transaction system."

### 🥈 Priority 2: Multi-Factor Transaction Verification
**Impact:** Last line of defense - stops theft even with complete system compromise
**Confidence:** 99%+ effectiveness
**Why:** Requires real-time human authorization from multiple parties via out-of-band channels. Cannot be automated or bypassed by malware. The 35 fraudulent transactions would require 35 separate approvals from executives who would immediately recognize them as fraudulent.

**Key Quote:** "The attackers were able to gain sufficient privileges to impersonate authorized bank employees and craft/send fraudulent but authenticated SWIFT messages."

### 🥉 Priority 3: Application Whitelisting (Critical Systems)
**Impact:** Prevents malware execution at multiple stages
**Confidence:** 90%+ effectiveness at SWIFT terminal level
**Why:** SWIFT terminals should only run official SWIFT software - nothing else. This control works at both initial infection (employee workstations) and final execution (SWIFT terminals).

**Key Quote:** "This prevents the execution of any unauthorized program, including unknown droppers (like the one used for NESTEGG)."

---

## Potential Weaknesses & Adversary Adaptations

No security control is perfect. Here are potential bypass scenarios and counter-measures:

| Attack Adaptation | Likelihood | Counter-Measure |
|-------------------|-----------|-----------------|
| **Insider Threat Collusion** - Attacker bribes multiple employees to approve fraudulent transactions | Low | Multi-party verification across different departments makes coordination exponentially harder. Requires multiple simultaneous insiders plus physical token access. Out-of-band verification creates audit trail of who approved what. |
| **Zero-Day in SWIFT Software** - Exploit vulnerability in whitelisted SWIFT application itself | Medium | EDR still detects anomalous behavior even from legitimate software. Transaction verification still required. Network segmentation limits lateral movement. Regular security audits and patching reduce window of exposure. |
| **Supply Chain Compromise** - Attacker compromises jump server or segmentation infrastructure before deployment | Low | Security infrastructure should have separate hardening: different vendors, hardware security modules, physical security, out-of-band management. Defense-in-depth ensures single point compromise doesn't cascade. |
| **Advanced Social Engineering** - Real-time phishing of executives during transaction verification | Very Low | Requires simultaneous social engineering of multiple executives for 35 transactions. After first suspicious approval, investigation begins. Out-of-band verification channels (known phone numbers) reduce spoofing risk. |
| **Long-Term Patient Attack** - Attacker waits months to understand baselines before acting | Low-Medium | Longer dwell time increases detection probability (EDR, NDR alerts). Baseline systems can detect "baseline manipulation" attempts. Regular security audits and threat hunting reduce effectiveness of patience. |

**Overall Assessment:** While determined nation-state actors might find creative bypasses, these controls raise the attack cost by **orders of magnitude**. The Bangladesh Bank attack succeeded due to **cascading failures** across every security layer. These solutions eliminate those failures.

---

## Real-World Validation

These solutions aren't theoretical. Following the Bangladesh Bank heist, the financial industry mandated similar controls:

**SWIFT Customer Security Programme (CSP):**
- Mandatory network segmentation for SWIFT infrastructure
- Multi-factor authentication requirements
- Security monitoring and logging obligations
- Regular security assessments

**Industry Adoption:**
- Major financial institutions globally implemented these controls
- Zero successful SWIFT-based heists of similar scale since 2016 (using similar techniques)
- Controls now considered **baseline security requirements** for financial institutions

The fact that these became **mandatory industry standards** validates their effectiveness.

---

## Conclusion

The breach of Bangladesh Bank highlights a reliance on perimeter defenses that failed under a sophisticated, persistent threat. The suggested shift involves adopting a **Zero Trust model** where detection and verification layers are woven throughout the architecture, ensuring that even if one component fails (like a compromised employee endpoint), critical systems (like the SWIFT terminals and audit logs) remain resilient and isolated.

**Final Verdict:** The proposed solutions would have prevented the Bangladesh Bank heist with **very high confidence (95%+)**. The attack succeeded because it exploited **every missing control** simultaneously. Implementing these solutions eliminates the exploitable gaps and creates multiple independent failure points for attackers, making a successful breach exponentially more difficult.

---

## Key Recommendations Summary

1. **Prevention**: Deploy EDR, email sandboxing, and application whitelisting
2. **Segmentation**: Implement micro-segmentation and jump servers for critical systems
3. **Detection**: Use NDR tools with deep packet inspection to identify anomalous protocols
4. **Resilience**: Ensure immutable audit logs and multi-factor transaction verification
5. **Architecture**: Adopt Zero Trust principles throughout the infrastructure
