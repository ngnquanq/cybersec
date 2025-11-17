# Bangladesh Bank Heist 2016 - Exercise Slide Content

## Slide 1: Title Slide
**Title:** Bangladesh Bank Heist 2016: A Case Study Analysis

**Subtitle:** Understanding the $81 Million Cyber Robbery and Lessons for Future Defense

**Key Visual Elements:**
- Bangladesh Bank logo area
- Date: February 4-5, 2016
- Amount Stolen: $81 Million
- Amount Blocked: $870 Million

---

## Slide 2: Executive Summary

**The Incident at a Glance:**

- **Date:** February 4-5, 2016
- **Target:** Bangladesh Bank (Central Bank of Bangladesh)
- **Attack Vector:** Malware + SWIFT Network Exploitation
- **Perpetrator:** Lazarus Group (North Korea-linked APT)
- **Amount Attempted:** $951 Million
- **Amount Stolen:** $81 Million
- **Amount Recovered:** $15 Million
- **Dwell Time:** 10 months undetected

**Critical Success Factors (for Attackers):**
1. Long-term persistence (10 months)
2. Deep understanding of SWIFT protocols
3. Custom malware development
4. Exploitation of weekend timing

**Critical Failure Points (for Defenders):**
1. Printer malfunction (ironically saved the day)
2. "Fandation" spelling error
3. Federal Reserve compliance vigilance

---

## Slide 3: Attack Timeline Overview

**Phase 1: Initial Compromise (January 2015)**
- Spear-phishing campaign
- Employee workstation infected
- Malware foothold established

**Phase 2: Lateral Movement (February - December 2015)**
- 10 months of reconnaissance
- Credential harvesting
- SWIFT system access achieved
- Network mapping completed

**Phase 3: Malware Deployment (Late January 2016)**
- Database manipulator installed
- SWIFT message generator deployed
- Printer suppression malware (malfunctioned)
- Log cleaning utilities positioned

**Phase 4: The Heist (February 4-5, 2016)**
- 35 fraudulent SWIFT messages sent
- $951 Million transfer attempts
- $81 Million successfully transferred

**Phase 5: Discovery (February 8, 2016)**
- Printer malfunction detected
- Investigation initiated within 90 minutes
- Federal Reserve notified
- $870 Million in pending transfers blocked

---

## Slide 4: Technical Attack Architecture

**Network Compromise Path:**

```
Internet
    ↓
Employee Workstation (Phishing)
    ↓
Corporate Network
    ↓
[NO SEGMENTATION]
    ↓
SWIFT Network
    ├─ SWIFT Alliance Access Servers
    ├─ SWIFT Database Servers
    └─ Printer Systems
```

**Critical Vulnerability:**
- SWIFT systems connected to corporate network
- No network segmentation or air-gapping
- Lateral movement enabled from office to SWIFT infrastructure

**Malware Components:**
1. **evtdiag.exe** - Database record manipulation
2. **SWIFT Message Generator** - Fraudulent MT103 creation
3. **Printer Malware** - Transaction evidence suppression (failed)
4. **Log Cleaner** - Forensic evidence removal

---

## Slide 5: The Printer Incident - The Unexpected Hero

**Normal SWIFT Operation:**
- Every SWIFT message → Automatic printed confirmation
- Printer serves as physical audit trail
- Daily operator review of printed logs

**Attacker's Plan:**
- Suppress only fraudulent transaction printouts
- Allow legitimate transactions to print normally
- Operators see "normal" activity

**What Actually Happened:**
- Printer malware malfunctioned
- ALL printing stopped completely
- Total printer silence = Immediate red flag

**Monday Morning, February 8:**
- 8:45 AM: Operators notice NO weekend printouts
- 9:00 AM: IT investigation begins
- 10:00 AM: Fraud discovered in manual log review
- 10:15 AM: Emergency response activated

**Impact:**
- ✓ $870 Million saved by printer failure
- ✓ Detection within 90 minutes of business reopening
- ✓ Prevented complete theft of $951 Million

---

## Slide 6: The "Fandation" Typo - Second Lucky Break

**The Suspicious Transfer:**
- Amount: $20,000,000
- Destination: Pan Asia Bank, Sri Lanka
- Beneficiary: Shalika **Fandation** [sic]

**Why It Mattered:**
1. Federal Reserve compliance officer noticed spelling error
2. Real organizations use correct spelling
3. Enhanced scrutiny triggered
4. No web presence found for "Shalika Fandation"
5. Bangladesh Bank closed for weekend (unable to confirm)
6. Transfer blocked pending clarification

**Result:** $20 Million saved by a simple typo

**Possible Origins:**
- Non-native English speaker error
- Translation/romanization issue
- Procedurally generated fictitious name
- Copy-paste error from source document

---

## Slide 7: Money Laundering Path

**The $81 Million Trail:**

**Stage 1: RCBC Bank (Philippines)**
- Four fictitious accounts opened
- Funds received from Federal Reserve NY
- Branch manager facilitated (later arrested)

**Stage 2: Solaire Resort & Casino**
- $66 Million transferred to casino accounts
- Converted to casino chips
- Minimal gambling (appearance only)
- Chips converted back to cash
- Creates "gambling winnings" legitimacy

**Stage 3: Distribution**
- Large cash withdrawals over several days
- Further layering through remittance services
- Real estate purchases
- Business investments
- Offshore accounts

**Recovery Status:**
- **$15 Million:** Frozen in casino accounts
- **$66 Million:** Disappeared into cash economy

**Why Philippines?**
- Casinos NOT covered by Anti-Money Laundering Council (at the time)
- Casino transactions exempt from financial reporting
- High-volume cash operations normal
- Easy to blend illicit funds

---

---

# SECTION 1: POLICY REVIEW (GRC ROLES)

---

## Slide 8: Policy Failures - Access Control Policies

**Existing Policy Gaps:**

**1. Password & Authentication Policies:**
- ❌ Weak password requirements
- ❌ No multi-factor authentication (MFA)
- ❌ Shared SWIFT operator credentials
- ❌ Infrequent credential rotation
- ❌ No session timeout enforcement

**2. Access Management:**
- ❌ No privileged access management (PAM)
- ❌ Insufficient segregation of duties
- ❌ No regular access reviews
- ❌ Excessive standing privileges

**3. Remote Access:**
- ❌ No clear remote access policy
- ❌ No VPN or secure access requirements
- ❌ After-hours access not monitored

**Impact on Incident:**
- Stolen credentials used for 10 months
- No detection of unauthorized access
- Attackers used legitimate credentials
- No alerts for unusual access patterns

---

## Slide 9: Policy Failures - Network Security Policies

**Critical Network Policy Gaps:**

**1. Network Segmentation:**
- ❌ No network segmentation policy enforced
- ❌ SWIFT systems on corporate network
- ❌ No air-gapping requirements
- ❌ Flat network architecture

**2. Firewall & DMZ Policies:**
- ❌ Insufficient firewall rules
- ❌ No DMZ for SWIFT infrastructure
- ❌ Overly permissive network access
- ❌ No zero-trust architecture

**3. Internet Access Policies:**
- ❌ SWIFT systems with internet access
- ❌ No whitelist-only approach
- ❌ Email accessible from SWIFT terminals

**Impact on Incident:**
- Phishing email reached employee workstation
- Malware spread from corporate to SWIFT network
- No barriers to lateral movement
- 10-month undetected presence

---

## Slide 10: Policy Failures - Monitoring & Detection Policies

**Monitoring Policy Gaps:**

**1. Logging & Audit Policies:**
- ❌ Insufficient log retention
- ❌ No centralized log management (SIEM)
- ❌ Critical events not logged
- ❌ No real-time log analysis

**2. Monitoring Requirements:**
- ❌ No 24/7 Security Operations Center (SOC)
- ❌ No intrusion detection systems (IDS/IPS)
- ❌ No anomaly detection capabilities
- ❌ No user behavior analytics (UEBA)

**3. Alerting Policies:**
- ❌ No critical alert definitions
- ❌ No after-hours access alerts
- ❌ No high-value transaction alerts
- ❌ No automated escalation procedures

**Impact on Incident:**
- 10-month dwell time undetected
- No alerts on suspicious activity
- Lateral movement invisible
- Malware deployment unnoticed

---

## Slide 11: Policy Failures - Incident Response & Business Continuity

**Incident Response Policy Gaps:**

**1. Incident Response Plan:**
- ❌ No documented IR plan
- ❌ No incident response team defined
- ❌ No escalation procedures
- ❌ No communication protocols

**2. Security Awareness:**
- ❌ No regular phishing training
- ❌ No social engineering awareness
- ❌ No security culture program
- ❌ No incident reporting procedures

**3. Business Continuity:**
- ❌ No weekend/holiday coverage plan
- ❌ No emergency contact procedures
- ❌ No 24/7 point of contact

**4. Third-Party Risk Management:**
- ❌ No SWIFT security requirements validation
- ❌ No vendor security assessments
- ❌ No supply chain security policies

**Impact on Incident:**
- Delayed detection (weekend timing exploited)
- No immediate response capability
- Employees fell for phishing
- Federal Reserve unable to reach Bangladesh Bank

---

## Slide 12: Proposed Policy Changes - Access Control

**Recommended Policy Improvements:**

**1. Enhanced Authentication Policy:**
- ✓ Mandatory MFA for ALL SWIFT access
- ✓ Hardware tokens or biometric authentication
- ✓ 16+ character password requirements
- ✓ 60-day password rotation (30-day for privileged)
- ✓ No password reuse (last 12 passwords)
- ✓ Account lockout after 3 failed attempts
- ✓ 15-minute idle session timeout

**2. Privileged Access Management Policy:**
- ✓ Implement PAM solution for SWIFT systems
- ✓ Just-in-time (JIT) privileged access
- ✓ Session recording for all privileged activities
- ✓ Approve-to-access for high-risk operations
- ✓ Eliminate shared accounts entirely
- ✓ Quarterly privileged access reviews

**3. Segregation of Duties Policy:**
- ✓ Define distinct roles: Initiator, Approver, Auditor
- ✓ No single person can complete high-value transaction
- ✓ Mandatory dual control for SWIFT operations
- ✓ Regular role assignment reviews

---

## Slide 13: Proposed Policy Changes - Network Security

**Recommended Network Security Policies:**

**1. Network Segmentation Policy:**
- ✓ SWIFT systems on isolated network segment
- ✓ Air-gapped or heavily restricted connectivity
- ✓ Jump box/bastion host with MFA for SWIFT access
- ✓ No direct connection from corporate to SWIFT network
- ✓ Zero-trust architecture principles

**2. Firewall & Access Control Policy:**
- ✓ Whitelist-only approach (deny by default)
- ✓ Explicit firewall rules for each permitted flow
- ✓ Regular firewall rule reviews (quarterly)
- ✓ Disable all unnecessary services and ports

**3. Internet & Email Policy:**
- ✓ No internet access from SWIFT terminals
- ✓ No email capability on SWIFT systems
- ✓ Dedicated SWIFT-only workstations
- ✓ Physical separation where possible

**4. Change Management Policy:**
- ✓ All SWIFT system changes require approval
- ✓ Change windows documented and monitored
- ✓ Rollback procedures documented
- ✓ Post-change validation required

---

## Slide 14: Proposed Policy Changes - Monitoring & Detection

**Recommended Monitoring Policies:**

**1. Logging & SIEM Policy:**
- ✓ Deploy enterprise SIEM solution
- ✓ 24/7 log monitoring and analysis
- ✓ Minimum 1-year log retention (SWIFT: 7 years)
- ✓ Real-time correlation and alerting
- ✓ Log sources: All SWIFT systems, firewalls, databases, authentication

**2. Intrusion Detection Policy:**
- ✓ Deploy IDS/IPS on SWIFT network perimeter
- ✓ Network traffic analysis (NTA) solution
- ✓ File integrity monitoring (FIM) on SWIFT systems
- ✓ Endpoint detection and response (EDR) on all endpoints

**3. Critical Alert Definitions:**
- ✓ After-hours SWIFT access → CRITICAL (immediate SMS)
- ✓ Transaction >$1M → HIGH (supervisor approval)
- ✓ >3 failed logins → MEDIUM (account lockout)
- ✓ Unusual transaction volume → HIGH (investigation)
- ✓ Database query anomaly → CRITICAL (potential block)
- ✓ **Printer failure >2 hours → HIGH (investigation)**
- ✓ New account creation on SWIFT → CRITICAL (review)
- ✓ Lateral movement indicators → HIGH (investigation)

**4. Behavioral Analytics Policy:**
- ✓ Implement UEBA solution
- ✓ Baseline normal user behavior
- ✓ Alert on deviations from baseline
- ✓ Machine learning for anomaly detection

---

## Slide 15: Proposed Policy Changes - Incident Response & Awareness

**Recommended IR & Awareness Policies:**

**1. Incident Response Plan:**
- ✓ Documented IR plan with defined phases
- ✓ Incident response team with clear roles
- ✓ 24/7 emergency contact procedures
- ✓ Escalation matrix (30min, 2hr, 24hr notifications)
- ✓ Communication templates pre-prepared
- ✓ Quarterly IR tabletop exercises
- ✓ Annual full-scale IR simulation

**2. Security Awareness Training Policy:**
- ✓ Mandatory annual security training
- ✓ Monthly security awareness topics
- ✓ Bi-weekly phishing simulations
- ✓ Metrics: <5% click rate, >80% reporting rate
- ✓ Remedial training for failures
- ✓ Positive reinforcement for reporting

**3. Operational Continuity Policy:**
- ✓ 24/7 SOC coverage (or outsourced)
- ✓ Weekend/holiday monitoring procedures
- ✓ Emergency escalation contacts updated quarterly
- ✓ Backup operators cross-trained

**4. Third-Party Risk Management:**
- ✓ Annual security assessments of SWIFT
- ✓ Vendor security questionnaires
- ✓ Right-to-audit clauses in contracts
- ✓ Supply chain security requirements

---

## Slide 16: Policy Compliance Framework Alignment

**Align with Industry Frameworks:**

**1. SWIFT Customer Security Controls Framework (CSCF):**
- ✓ Implement all 31 mandatory and advisory controls
- ✓ Annual self-attestation to SWIFT
- ✓ Independent third-party assessment
- ✓ Continuous compliance monitoring

**2. NIST Cybersecurity Framework:**
- ✓ IDENTIFY: Asset management, risk assessment
- ✓ PROTECT: Access control, awareness, data security
- ✓ DETECT: Anomalies, continuous monitoring
- ✓ RESPOND: Response planning, communications
- ✓ RECOVER: Recovery planning, improvements

**3. ISO 27001/27002:**
- ✓ Information security management system (ISMS)
- ✓ Risk-based approach to security controls
- ✓ Regular audits and certifications

**4. PCI-DSS (if applicable):**
- ✓ Cardholder data protection
- ✓ Network segmentation requirements
- ✓ Regular security testing

**Policy Governance:**
- Annual policy reviews and updates
- Executive sponsorship and board oversight
- Regular compliance audits
- Metrics and KPIs for policy effectiveness

---

---

# SECTION 2: TECHNICAL BASELINE REVIEW (SOFTWARE DEVELOPMENT ROLES)

---

## Slide 17: Technical Baseline - Existing Security Measures

**Bangladesh Bank's Technical Environment (Pre-Incident):**

**1. SWIFT Infrastructure:**
- SWIFT Alliance Access software (older version)
- Oracle database for transaction records
- Windows-based SWIFT terminals
- Dedicated printer systems for audit trails

**2. Network Architecture:**
- Corporate network connected to SWIFT network
- No network segmentation
- Basic firewall (insufficient rules)
- No DMZ for critical systems

**3. Security Controls:**
- Basic antivirus (signature-based only)
- No intrusion detection systems
- No SIEM or centralized logging
- No endpoint detection and response
- No network traffic analysis

**4. Access Controls:**
- Username/password authentication only
- No multi-factor authentication
- Shared operator credentials
- No privileged access management

**Critical Weakness:** Lack of defense-in-depth architecture

---

## Slide 18: Technical Failures - Network Architecture

**Network Architecture Vulnerabilities:**

**Actual Architecture:**
```
Internet → Firewall → Corporate Network → SWIFT Network
                     (Email/Workstations)  (SWIFT Terminals)
                              ↓
                    DIRECT CONNECTION
                    (No segmentation)
```

**Critical Flaws:**
1. ❌ No network segmentation between corporate and SWIFT
2. ❌ SWIFT terminals on same network as email workstations
3. ❌ Single firewall, no defense-in-depth
4. ❌ No air-gapping of critical systems
5. ❌ Flat network architecture

**Attack Exploitation:**
- Phishing email → Corporate workstation
- Lateral movement → SWIFT network
- No barriers encountered
- 10-month dwell time undetected

**Ideal Architecture:**
```
Internet → Perimeter FW → DMZ → Internal FW → Corporate Network

                                               ❌ NO CONNECTION ❌

                          Jump Box (MFA) → SWIFT FW → ISOLATED SWIFT Network
```

---

## Slide 19: Technical Failures - Endpoint Security

**Endpoint Protection Deficiencies:**

**1. Antivirus Limitations:**
- ❌ Signature-based detection only
- ❌ No behavioral analysis
- ❌ Easily bypassed by custom malware
- ❌ No advanced threat protection

**2. Missing Endpoint Controls:**
- ❌ No Endpoint Detection and Response (EDR)
- ❌ No application whitelisting
- ❌ No host-based intrusion prevention
- ❌ No memory protection
- ❌ No sandboxing for suspicious files

**3. Configuration Weaknesses:**
- ❌ Outdated operating systems
- ❌ Unpatched vulnerabilities
- ❌ No hardening standards
- ❌ Unnecessary services running
- ❌ Local admin rights widespread

**4. Email Security:**
- ❌ No advanced email filtering
- ❌ No attachment sandboxing
- ❌ No URL rewriting/scanning
- ❌ No DMARC/SPF/DKIM validation

**Impact:** Custom Lazarus malware bypassed all endpoint defenses

---

## Slide 20: Technical Failures - Database & Application Security

**SWIFT Database Vulnerabilities:**

**1. Database Security:**
- ❌ Database accessible from multiple systems
- ❌ No database activity monitoring (DAM)
- ❌ Insufficient access controls
- ❌ No real-time query analysis
- ❌ No database firewall

**2. SWIFT Alliance Access:**
- ❌ Older software version (unpatched)
- ❌ No integrity monitoring
- ❌ No application-level controls
- ❌ API/DLL injection possible

**3. Authentication to Database:**
- ❌ Weak database credentials
- ❌ Embedded passwords in application
- ❌ No credential vaulting
- ❌ No encryption of credentials at rest

**4. Audit & Logging:**
- ❌ Insufficient database audit logging
- ❌ No tamper-proof log storage
- ❌ Logs stored locally (deletable)
- ❌ No real-time log forwarding

**Malware Exploitation:**
- evtdiag.exe injected into database process
- Manipulated query results to hide fraudulent transactions
- Altered database records without detection

---

## Slide 21: Technical Failures - Monitoring & Detection Systems

**Missing Detection Capabilities:**

**1. No SIEM Solution:**
- ❌ No centralized log collection
- ❌ No correlation of events across systems
- ❌ No real-time alerting
- ❌ No threat intelligence integration
- ❌ No historical analysis capability

**2. No Intrusion Detection:**
- ❌ No network IDS/IPS
- ❌ No host-based IDS
- ❌ No anomaly detection
- ❌ No lateral movement detection

**3. No Behavioral Analytics:**
- ❌ No user behavior baselines
- ❌ No entity behavior analytics
- ❌ No machine learning detection
- ❌ No anomalous transaction detection

**4. No Network Monitoring:**
- ❌ No network traffic analysis (NTA)
- ❌ No NetFlow collection
- ❌ No DNS monitoring
- ❌ No command & control detection

**Result:** 10-month dwell time with zero detection

---

## Slide 22: Proposed Technical Improvements - Network Architecture

**Recommended Network Architecture:**

**1. Network Segmentation:**
```
[Internet]
    ↓
[Perimeter Firewall + IPS]
    ↓
[DMZ - Public Services]
    ↓
[Internal Firewall]
    ↓
[Corporate Network]
    ↓
❌ NO DIRECT PATH ❌
    ↓
[Jump Box/Bastion Host]
  - MFA required
  - Session recording
  - Audit logging
    ↓
[SWIFT Network Firewall]
    ↓
[ISOLATED SWIFT NETWORK]
  - SWIFT terminals (no email/internet)
  - SWIFT Alliance Access servers
  - SWIFT database servers
  - Printer systems
```

**2. Technical Implementation:**
- ✓ VLANs for network segmentation
- ✓ Firewall rules: whitelist-only (deny by default)
- ✓ Micro-segmentation within SWIFT network
- ✓ East-west traffic inspection
- ✓ Zero-trust network architecture

**3. Access Control:**
- ✓ Jump box with MFA for SWIFT access
- ✓ Session recording and keystroke logging
- ✓ No direct SSH/RDP to SWIFT systems
- ✓ Breakglass procedures for emergencies

---

## Slide 23: Proposed Technical Improvements - Endpoint Security

**Recommended Endpoint Protection:**

**1. Advanced Endpoint Protection:**
- ✓ Next-generation antivirus (NGAV)
- ✓ Endpoint Detection and Response (EDR)
  - CrowdStrike Falcon
  - Carbon Black
  - SentinelOne
  - Microsoft Defender ATP
- ✓ Behavioral analysis and AI/ML detection
- ✓ Automated threat hunting
- ✓ Fileless malware detection

**2. Application Control:**
- ✓ Application whitelisting (only approved apps run)
- ✓ Code signing verification
- ✓ DLL injection prevention
- ✓ Memory protection (DEP, ASLR)

**3. Email Security:**
- ✓ Advanced email gateway with sandboxing
- ✓ URL rewriting and detonation
- ✓ Attachment sandboxing
- ✓ DMARC/SPF/DKIM enforcement
- ✓ AI-based phishing detection

**4. System Hardening:**
- ✓ OS patching within 7 days (critical: 24 hours)
- ✓ CIS Benchmarks for hardening
- ✓ Disable unnecessary services
- ✓ Remove local admin rights
- ✓ Full disk encryption

---

## Slide 24: Proposed Technical Improvements - SWIFT Security

**Recommended SWIFT-Specific Controls:**

**1. SWIFT Alliance Access Security:**
- ✓ Upgrade to latest SWIFT software version
- ✓ Dedicated hardware for SWIFT (no dual-use)
- ✓ File integrity monitoring (FIM) on SWIFT systems
- ✓ Application whitelisting
- ✓ Hardware Security Module (HSM) for key management

**2. Database Security:**
- ✓ Database Activity Monitoring (DAM)
- ✓ Real-time query analysis and blocking
- ✓ Database firewall (Oracle AVDF or similar)
- ✓ Encryption at rest and in transit
- ✓ Privileged account monitoring
- ✓ Tamper-proof audit logs (WORM storage)

**3. Transaction Integrity:**
- ✓ Real-time transaction validation
- ✓ Anomaly detection for unusual transactions
- ✓ Automated alerts for high-value transfers
- ✓ Dual approval for transactions >$1M
- ✓ Rate limiting (max transactions per hour)

**4. Printer & Audit Systems:**
- ✓ Redundant printer systems
- ✓ Automated printer health monitoring
- ✓ Alert on printer failures within 30 minutes
- ✓ Electronic + physical audit trails
- ✓ Daily reconciliation procedures

---

## Slide 25: Proposed Technical Improvements - Monitoring & Detection

**Recommended Detection Architecture:**

**1. SIEM Solution:**
- ✓ Enterprise SIEM deployment
  - Splunk Enterprise Security
  - IBM QRadar
  - LogRhythm
  - Elastic SIEM
- ✓ Log sources: All SWIFT systems, firewalls, databases, endpoints, authentication
- ✓ Real-time correlation and alerting
- ✓ 24/7 SOC monitoring (or outsourced)
- ✓ Threat intelligence integration

**2. Network Detection:**
- ✓ Network IDS/IPS (Snort, Suricata, Cisco Firepower)
- ✓ Network traffic analysis (Zeek, Darktrace)
- ✓ NetFlow collection and analysis
- ✓ DNS monitoring and filtering
- ✓ TLS/SSL inspection

**3. Behavioral Analytics:**
- ✓ User and Entity Behavior Analytics (UEBA)
- ✓ Baseline normal behavior per user/system
- ✓ Machine learning anomaly detection
- ✓ Automated threat hunting

**4. Threat Intelligence:**
- ✓ Integration with threat feeds
- ✓ IOC matching and blocking
- ✓ FS-ISAC membership and intelligence sharing
- ✓ MITRE ATT&CK framework mapping

---

## Slide 26: Proposed Technical Improvements - Authentication & Access

**Recommended Authentication Architecture:**

**1. Multi-Factor Authentication:**
- ✓ MFA for ALL SWIFT access (mandatory)
- ✓ Hardware tokens (YubiKey, RSA SecurID)
- ✓ Biometric authentication (fingerprint, facial recognition)
- ✓ No SMS-based MFA (vulnerable to SIM swap)

**2. Privileged Access Management (PAM):**
- ✓ PAM solution deployment
  - CyberArk
  - BeyondTrust
  - Thycotic
- ✓ Credential vaulting (no embedded passwords)
- ✓ Just-in-time (JIT) access
- ✓ Session recording and monitoring
- ✓ Automated credential rotation

**3. Identity & Access Management:**
- ✓ Single Sign-On (SSO) with MFA
- ✓ Role-based access control (RBAC)
- ✓ Principle of least privilege
- ✓ Regular access reviews (quarterly)
- ✓ Automated deprovisioning

**4. Access Monitoring:**
- ✓ Real-time session monitoring
- ✓ Keystroke logging for privileged sessions
- ✓ After-hours access alerts
- ✓ Impossible travel detection
- ✓ Concurrent session detection

---

## Slide 27: Proposed Technical Improvements - Incident Response Tech

**Recommended IR Technology Stack:**

**1. Forensic Capabilities:**
- ✓ Memory forensics tools (Volatility, Rekall)
- ✓ Disk forensics tools (EnCase, FTK, Autopsy)
- ✓ Network forensics (Wireshark, NetworkMiner)
- ✓ Malware analysis sandbox (Cuckoo, Any.run)
- ✓ Reverse engineering tools (IDA Pro, Ghidra)

**2. IR Automation:**
- ✓ Security Orchestration, Automation, and Response (SOAR)
  - Splunk Phantom
  - Palo Alto Cortex XSOAR
  - IBM Resilient
- ✓ Automated playbooks for common scenarios
- ✓ Automated containment actions
- ✓ Ticketing integration (ServiceNow, Jira)

**3. Evidence Preservation:**
- ✓ Automated memory dumping on alert
- ✓ Network packet capture (PCAP) retention
- ✓ Immutable log storage (WORM)
- ✓ Forensic imaging procedures
- ✓ Chain of custody documentation

**4. Communication Tools:**
- ✓ Secure incident communication platform
- ✓ Encrypted messaging for IR team
- ✓ War room collaboration tools
- ✓ Status dashboards for executives

---

## Slide 28: Technical Implementation Roadmap

**Phased Implementation Plan:**

**Phase 1: Critical (0-3 Months) - $2-3M**
- ✓ Deploy MFA for SWIFT access (Immediate)
- ✓ Implement network segmentation (isolate SWIFT)
- ✓ Deploy EDR on all endpoints
- ✓ Implement SIEM with critical use cases
- ✓ Enable database activity monitoring
- ✓ Deploy PAM for privileged accounts

**Phase 2: High Priority (3-6 Months) - $3-5M**
- ✓ Full SIEM deployment with 24/7 SOC
- ✓ Network IDS/IPS deployment
- ✓ Email security gateway with sandboxing
- ✓ File integrity monitoring on SWIFT systems
- ✓ Application whitelisting
- ✓ Upgrade SWIFT software to latest version

**Phase 3: Important (6-12 Months) - $2-3M**
- ✓ UEBA deployment
- ✓ Network traffic analysis (NTA)
- ✓ SOAR platform for IR automation
- ✓ Advanced threat intelligence integration
- ✓ Red team / purple team exercises
- ✓ IR automation and playbooks

**Phase 4: Enhancement (12-24 Months) - $1-2M**
- ✓ AI/ML-based anomaly detection
- ✓ Deception technology (honeypots)
- ✓ Advanced forensic capabilities
- ✓ Security maturity improvements
- ✓ Continuous testing and improvement

**Total Estimated Cost:** $8-13M over 24 months

---

## Slide 29: Technical Metrics & KPIs

**Measuring Technical Effectiveness:**

**1. Detection Metrics:**
- Mean Time to Detect (MTTD): Target <1 hour
- Mean Time to Respond (MTTR): Target <4 hours
- Mean Time to Contain (MTTC): Target <24 hours
- False Positive Rate: Target <5%
- Detection Coverage: Target >95% of MITRE ATT&CK techniques

**2. Prevention Metrics:**
- Phishing simulation click rate: Target <5%
- Patch compliance: Target >95% within SLA
- MFA adoption: Target 100% for SWIFT systems
- Vulnerability remediation: Critical <7 days, High <30 days
- Endpoint protection coverage: Target 100%

**3. Operational Metrics:**
- SIEM log ingestion: Target >99% uptime
- SOC alert triage time: Target <15 minutes
- Incident escalation time: Target <30 minutes
- Backup success rate: Target 100%
- System availability: Target >99.9% for SWIFT

**4. Compliance Metrics:**
- SWIFT CSCF compliance: 100% of mandatory controls
- Audit findings: Target 0 critical, <5 high
- Policy compliance: Target >95%
- Training completion: Target 100% annual

---

---

# SECTION 3: OPERATIONAL PROCESS REVIEW (OPERATIONS ROLES)

---

## Slide 30: Operational Process Failures - Daily Operations

**Pre-Incident Operational Weaknesses:**

**1. Transaction Processing:**
- ❌ No dual approval for high-value transactions
- ❌ Insufficient transaction validation
- ❌ No real-time reconciliation
- ❌ No automated anomaly checks
- ❌ Weekend processing gaps

**2. Monitoring & Surveillance:**
- ❌ No 24/7 monitoring coverage
- ❌ Weekend/holiday gaps in monitoring
- ❌ No real-time transaction monitoring
- ❌ Manual daily reconciliation only
- ❌ No automated alerting

**3. Physical Security:**
- ❌ Insufficient SWIFT terminal room security
- ❌ No video surveillance reviewed regularly
- ❌ Badge access not monitored
- ❌ No separation of SWIFT operations

**4. Documentation:**
- ❌ Incomplete operational procedures
- ❌ No change management process
- ❌ Inadequate audit trails
- ❌ No review of printed confirmations

**Impact:** Attackers exploited weekend gaps and lack of continuous monitoring

---

## Slide 31: Operational Process Failures - Change Management

**Change Management Weaknesses:**

**1. System Changes:**
- ❌ No formal change approval process
- ❌ Changes implemented without documentation
- ❌ No testing environment for SWIFT changes
- ❌ No rollback procedures
- ❌ No post-change validation

**2. Access Changes:**
- ❌ New accounts created without approval
- ❌ No regular access reviews
- ❌ Terminated employees not deprovisioned timely
- ❌ No logging of access changes

**3. Configuration Management:**
- ❌ No baseline configuration documented
- ❌ Configuration drift not detected
- ❌ No configuration backup and recovery
- ❌ No integrity checking

**4. Patching & Updates:**
- ❌ Irregular patching schedule
- ❌ SWIFT software outdated
- ❌ No patch testing process
- ❌ Critical vulnerabilities not prioritized

**How Attackers Exploited:**
- Malware installed without detection
- New backdoor accounts created
- Configuration changes went unnoticed
- System modifications for 10 months

---

## Slide 32: Operational Process Failures - Incident Response

**Incident Response Operational Gaps:**

**1. Detection & Reporting:**
- ❌ No incident reporting procedures
- ❌ No defined incident severity levels
- ❌ Employees unsure how to report suspicious activity
- ❌ No 24/7 incident hotline

**2. Response Procedures:**
- ❌ No documented IR playbooks
- ❌ No defined roles and responsibilities
- ❌ No escalation matrix
- ❌ No communication templates
- ❌ No evidence preservation procedures

**3. Coordination:**
- ❌ No coordination with Federal Reserve
- ❌ No emergency contact list maintained
- ❌ Weekend/holiday contact gaps
- ❌ No pre-established law enforcement relationships

**4. Recovery:**
- ❌ No disaster recovery plan tested
- ❌ No business continuity procedures
- ❌ No backup validation
- ❌ No restoration time objectives

**Real Impact:** Discovery delayed by weekend; Federal Reserve unable to reach Bangladesh Bank for confirmation

---

## Slide 33: Operational Process Failures - Training & Awareness

**Training & Awareness Gaps:**

**1. Security Training:**
- ❌ No regular security awareness training
- ❌ No phishing simulation exercises
- ❌ SWIFT operators not trained on threats
- ❌ No specialized training for high-risk roles

**2. Operational Training:**
- ❌ Inadequate SWIFT operations training
- ❌ No cross-training for backup operators
- ❌ Procedures not documented
- ❌ No refresher training

**3. Incident Response Training:**
- ❌ No IR tabletop exercises
- ❌ Staff unaware of IR procedures
- ❌ No simulation drills
- ❌ No lessons learned reviews

**4. Compliance Training:**
- ❌ No SWIFT security requirements training
- ❌ Compliance obligations not understood
- ❌ No regulatory update training

**Result:** Employees fell for phishing; operators missed early warning signs; delayed incident recognition

---

## Slide 34: Proposed Operational Improvements - Daily Operations

**Recommended Daily Operational Procedures:**

**1. Transaction Processing Controls:**
- ✓ Dual approval for transactions >$500K
- ✓ Mandatory supervisor approval >$1M
- ✓ Real-time transaction validation
- ✓ Automated anomaly detection
- ✓ Hourly reconciliation during business hours
- ✓ Daily balance verification with Federal Reserve

**2. Monitoring Procedures:**
- ✓ 24/7 SOC monitoring (in-house or outsourced)
- ✓ Real-time SIEM dashboard review
- ✓ Hourly SWIFT system health checks
- ✓ Daily printer functionality verification
- ✓ Weekend and holiday coverage plan

**3. Physical Security Procedures:**
- ✓ SWIFT operations in locked, dedicated room
- ✓ Badge access with two-person rule
- ✓ Video surveillance with review
- ✓ Daily access log review
- ✓ Visitor log and escort requirements

**4. Audit & Documentation:**
- ✓ Daily review of printed SWIFT confirmations
- ✓ Comparison of screen vs. printed records
- ✓ Documentation of all exceptions
- ✓ Weekly reconciliation reports to management
- ✓ Monthly audit of SWIFT activities

---

## Slide 35: Proposed Operational Improvements - Change Management

**Recommended Change Management Process:**

**1. Change Request & Approval:**
- ✓ Formal change request form
- ✓ Business justification required
- ✓ Risk assessment for each change
- ✓ Change Advisory Board (CAB) approval
- ✓ Executive approval for SWIFT changes

**2. Testing & Validation:**
- ✓ Dedicated test environment for SWIFT
- ✓ Test plan for each change
- ✓ User acceptance testing (UAT)
- ✓ Security validation before production
- ✓ Rollback plan documented and tested

**3. Implementation:**
- ✓ Scheduled change windows
- ✓ Pre-implementation checklist
- ✓ Real-time monitoring during change
- ✓ Post-implementation validation
- ✓ Documentation updated

**4. Emergency Changes:**
- ✓ Emergency change process defined
- ✓ Required approvals (CIO, CISO)
- ✓ Accelerated but documented process
- ✓ Post-implementation review

**5. Access Management:**
- ✓ Formal access request and approval
- ✓ Quarterly access reviews
- ✓ Automated deprovisioning upon termination
- ✓ Recertification of privileged access (quarterly)

---

## Slide 36: Proposed Operational Improvements - Incident Response

**Recommended IR Operational Procedures:**

**1. Detection & Reporting:**
- ✓ 24/7 incident hotline
- ✓ Web-based incident reporting form
- ✓ Defined incident severity levels (P1-P4)
- ✓ Mandatory reporting within 15 minutes
- ✓ "See something, say something" culture

**2. Incident Response Playbooks:**

**Playbook 1: Suspicious SWIFT Transaction**
```
1. Immediately notify SWIFT supervisor (5 min)
2. SWIFT supervisor contacts Federal Reserve (10 min)
3. Freeze related accounts (15 min)
4. Activate IR team (20 min)
5. Preserve evidence (30 min)
6. Initiate investigation (ongoing)
```

**Playbook 2: Malware Detection**
```
1. Isolate affected system from network (immediate)
2. Capture memory dump (5 min)
3. Notify SOC and IR team (10 min)
4. Begin forensic analysis (30 min)
5. Scope additional compromised systems (1 hour)
6. Eradication and recovery (ongoing)
```

**Playbook 3: Unauthorized Access**
```
1. Disable compromised account (immediate)
2. Review access logs (15 min)
3. Identify affected systems (30 min)
4. Force password reset for related accounts (1 hour)
5. Investigate root cause (ongoing)
```

---

## Slide 37: Proposed Operational Improvements - Communication

**Recommended Communication Procedures:**

**1. Internal Communication Matrix:**

| Incident Severity | Notification Time | Stakeholders | Method |
|-------------------|-------------------|--------------|--------|
| **P1 - Critical** | Immediate | CISO, CIO, CEO, Board | Phone + SMS |
| **P2 - High** | 30 minutes | CISO, CIO, Department Heads | Phone + Email |
| **P3 - Medium** | 2 hours | CISO, IT Manager | Email |
| **P4 - Low** | 24 hours | Security Team | Ticket |

**2. External Communication:**
- ✓ Federal Reserve: 24/7 hotline established
- ✓ SWIFT organization: Secure communication channel
- ✓ Law enforcement: Pre-established contacts
- ✓ Regulators: Notification within 24 hours
- ✓ Customers: Transparent communication if affected

**3. Crisis Communication:**
- ✓ Designated spokesperson (trained)
- ✓ Pre-approved message templates
- ✓ Legal review of external statements
- ✓ Media handling procedures
- ✓ Social media monitoring and response

**4. Emergency Contact List:**
- ✓ Maintained and updated quarterly
- ✓ Primary and backup contacts
- ✓ Multiple contact methods (phone, email, SMS)
- ✓ Contact list tested quarterly
- ✓ 24/7 availability verified

---

## Slide 38: Proposed Operational Improvements - Business Continuity

**Recommended Business Continuity Procedures:**

**1. Weekend & Holiday Operations:**
- ✓ On-call SWIFT operator (rotating schedule)
- ✓ 24/7 SOC monitoring coverage
- ✓ Emergency escalation procedures
- ✓ Backup contact list for Federal Reserve
- ✓ Regular communication tests

**2. Disaster Recovery:**
- ✓ Documented DR plan for SWIFT systems
- ✓ Recovery Time Objective (RTO): <4 hours
- ✓ Recovery Point Objective (RPO): <1 hour
- ✓ Quarterly DR testing
- ✓ Alternate processing site identified

**3. Backup Procedures:**
- ✓ Daily incremental backups
- ✓ Weekly full backups
- ✓ Offsite backup storage
- ✓ Monthly backup restoration tests
- ✓ Immutable backup copies (ransomware protection)

**4. Critical System Redundancy:**
- ✓ Redundant SWIFT terminals
- ✓ Redundant printer systems
- ✓ Failover database servers
- ✓ Redundant network paths
- ✓ UPS and generator backup power

---

## Slide 39: Proposed Operational Improvements - Training Program

**Recommended Training & Awareness Program:**

**1. Security Awareness Training:**

**Monthly Topics:**
- Month 1: Phishing identification and reporting
- Month 2: Social engineering (phone, email, in-person)
- Month 3: Password security and MFA
- Month 4: Physical security awareness
- Month 5: Incident reporting procedures
- Month 6: Data classification and handling
- Month 7: SWIFT-specific threats
- Month 8: Insider threat awareness
- Month 9: Mobile device security
- Month 10: Cloud security
- Month 11: Compliance requirements
- Month 12: Year in review and advanced topics

**2. Phishing Simulation Program:**
- ✓ Bi-weekly random phishing tests
- ✓ Metrics tracked: Click rate, credential submission, reporting rate
- ✓ Target: <5% click rate, >80% reporting rate
- ✓ Remedial training for failures
- ✓ Recognition for consistent reporters

**3. Role-Specific Training:**

**SWIFT Operators:**
- ✓ SWIFT security requirements (annual)
- ✓ Transaction validation procedures (quarterly)
- ✓ Incident recognition and reporting (semi-annual)
- ✓ Operational procedures refresher (annual)

**IT Administrators:**
- ✓ Secure configuration management (annual)
- ✓ Incident response procedures (semi-annual)
- ✓ Forensic data collection (annual)
- ✓ Security tool training (as needed)

**Executives:**
- ✓ Cyber risk awareness (annual)
- ✓ Incident communication (annual)
- ✓ Regulatory requirements (annual)

---

## Slide 40: Proposed Operational Improvements - Continuous Improvement

**Recommended Continuous Improvement Process:**

**1. Regular Testing & Exercises:**

**Quarterly:**
- ✓ Tabletop incident response exercises
- ✓ Disaster recovery testing
- ✓ Backup restoration validation
- ✓ Emergency communication drills

**Semi-Annual:**
- ✓ Red team penetration testing
- ✓ Social engineering assessments
- ✓ Physical security audits
- ✓ Access review and recertification

**Annual:**
- ✓ Full-scale IR simulation
- ✓ Business continuity exercise
- ✓ Third-party security assessment
- ✓ Compliance audit (SWIFT CSCF)

**2. Metrics & Reporting:**
- ✓ Weekly operational security metrics
- ✓ Monthly executive dashboard
- ✓ Quarterly board reporting
- ✓ Annual security posture assessment

**3. Lessons Learned:**
- ✓ Post-incident review (every incident)
- ✓ Capture lessons and action items
- ✓ Update procedures based on findings
- ✓ Share lessons across organization

**4. External Engagement:**
- ✓ FS-ISAC membership and participation
- ✓ SWIFT user group engagement
- ✓ Industry conference attendance
- ✓ Peer organization collaboration

---

---

# SECTION 4: CONSOLIDATED RECOMMENDATIONS

---

## Slide 41: Summary of Key Recommendations - Policy (GRC)

**Critical Policy Improvements:**

**1. Access Control Policies:**
- ✓ Mandatory MFA for all SWIFT access
- ✓ Privileged Access Management (PAM)
- ✓ Segregation of duties enforcement
- ✓ Regular access reviews and recertification

**2. Network Security Policies:**
- ✓ Network segmentation and isolation
- ✓ Zero-trust architecture
- ✓ Firewall whitelist-only approach
- ✓ No internet access from SWIFT terminals

**3. Monitoring & Detection Policies:**
- ✓ 24/7 SIEM monitoring
- ✓ Critical alert definitions
- ✓ Behavioral analytics implementation
- ✓ Threat intelligence integration

**4. Incident Response Policies:**
- ✓ Documented IR plan with playbooks
- ✓ 24/7 emergency procedures
- ✓ Regular testing and exercises
- ✓ Security awareness training program

**5. Compliance Framework:**
- ✓ SWIFT CSCF compliance (31 controls)
- ✓ NIST CSF alignment
- ✓ ISO 27001/27002 certification
- ✓ Annual audits and assessments

---

## Slide 42: Summary of Key Recommendations - Technical (Software Dev)

**Critical Technical Improvements:**

**1. Network Architecture:**
- ✓ Isolated SWIFT network with jump box access
- ✓ Defense-in-depth with multiple firewall layers
- ✓ Micro-segmentation within SWIFT environment
- ✓ Zero-trust network principles

**2. Endpoint Security:**
- ✓ Next-gen EDR on all endpoints
- ✓ Application whitelisting
- ✓ Advanced email security with sandboxing
- ✓ System hardening to CIS benchmarks

**3. SWIFT-Specific Security:**
- ✓ Latest SWIFT software versions
- ✓ Database activity monitoring
- ✓ File integrity monitoring
- ✓ Redundant printer systems with monitoring
- ✓ Transaction anomaly detection

**4. Detection & Monitoring:**
- ✓ Enterprise SIEM with 24/7 SOC
- ✓ Network IDS/IPS deployment
- ✓ User and Entity Behavior Analytics
- ✓ Automated threat hunting

**5. Authentication & Access:**
- ✓ MFA with hardware tokens
- ✓ PAM solution for privileged access
- ✓ Just-in-time access provisioning
- ✓ Session recording and monitoring

**Estimated Investment:** $8-13M over 24 months

---

## Slide 43: Summary of Key Recommendations - Operations

**Critical Operational Improvements:**

**1. Daily Operations:**
- ✓ Dual approval for high-value transactions
- ✓ Real-time transaction validation
- ✓ 24/7 monitoring coverage
- ✓ Daily printer and system health checks
- ✓ Continuous reconciliation procedures

**2. Change Management:**
- ✓ Formal change approval process
- ✓ Testing in dedicated environment
- ✓ Documented rollback procedures
- ✓ Quarterly access reviews

**3. Incident Response:**
- ✓ 24/7 incident hotline
- ✓ Documented IR playbooks
- ✓ Defined escalation procedures
- ✓ Regular IR exercises and drills

**4. Business Continuity:**
- ✓ Weekend/holiday coverage plan
- ✓ Disaster recovery with quarterly testing
- ✓ Backup validation and restoration
- ✓ Emergency communication procedures

**5. Training & Awareness:**
- ✓ Monthly security awareness training
- ✓ Bi-weekly phishing simulations
- ✓ Role-specific training programs
- ✓ Annual refresher and advanced training

---

## Slide 44: Implementation Priority Matrix

**Prioritized Implementation Plan:**

**IMMEDIATE (0-30 Days) - Critical Security Gaps:**
1. Deploy MFA for SWIFT access
2. Disable internet access from SWIFT terminals
3. Implement emergency monitoring procedures
4. Establish 24/7 incident hotline
5. Create emergency contact list

**HIGH PRIORITY (1-3 Months) - Major Vulnerabilities:**
1. Network segmentation (isolate SWIFT)
2. Deploy EDR on all endpoints
3. Implement basic SIEM with critical alerts
4. Deploy PAM for privileged accounts
5. Establish formal change management
6. Begin security awareness training

**MEDIUM PRIORITY (3-6 Months) - Strengthen Defenses:**
1. Full SIEM deployment with 24/7 SOC
2. Network IDS/IPS
3. Database activity monitoring
4. Email security gateway
5. File integrity monitoring
6. IR playbook development and testing

**ONGOING (6-24 Months) - Maturity Enhancement:**
1. UEBA deployment
2. Advanced threat intelligence
3. SOAR platform
4. Continuous testing and improvement
5. Compliance certifications
6. Red team exercises

---

## Slide 45: Cost-Benefit Analysis

**Investment vs. Risk Reduction:**

**Total Estimated Investment:**
- Year 1: $6-9M
- Year 2: $2-4M
- Ongoing Annual: $3-5M (staff, licenses, SOC)

**Risk Reduction:**
- **Prevented Loss (Bangladesh example):** $870M saved by printer failure
- **Actual Loss:** $81M stolen
- **Potential Loss (no safeguards):** $951M

**ROI Calculation:**
- Investment: $10-15M over 2 years
- Risk Mitigation: $500M-1B+ (potential future attacks prevented)
- **ROI: 3,300% - 6,600%+**

**Intangible Benefits:**
- Reputation protection
- Regulatory compliance
- Customer confidence
- Operational resilience
- Competitive advantage

**Cost of Inaction:**
- Potential complete loss of reserves
- Regulatory fines and penalties
- Loss of international banking access
- Reputation damage (irreparable)
- Legal liability
- Executive/board consequences

**Conclusion:** Security investment is insurance against catastrophic loss

---

## Slide 46: Compliance & Regulatory Alignment

**Meeting Industry Standards:**

**SWIFT Customer Security Controls Framework (CSCF):**
- ✓ All 31 controls addressed in recommendations
- ✓ Annual self-attestation prepared
- ✓ Independent assessment planned
- ✓ Continuous compliance monitoring

**NIST Cybersecurity Framework:**
- ✓ IDENTIFY: Asset management, risk assessment
- ✓ PROTECT: Access control, awareness, data security, protective technology
- ✓ DETECT: Anomalies, continuous monitoring
- ✓ RESPOND: Response planning, communications, analysis
- ✓ RECOVER: Recovery planning, improvements, communications

**Other Applicable Frameworks:**
- ✓ ISO 27001: Information Security Management
- ✓ COBIT: Governance and management of enterprise IT
- ✓ PCI-DSS: Payment card data protection (if applicable)
- ✓ Local regulations: Bangladesh Bank regulations, ICT Act

**Audit & Certification Plan:**
- Year 1: Gap assessment and remediation
- Year 2: Third-party audit preparation
- Year 3: ISO 27001 certification
- Ongoing: Annual compliance audits

---

## Slide 47: Key Performance Indicators (KPIs)

**Measuring Success:**

**Security KPIs:**
- Mean Time to Detect (MTTD): <1 hour
- Mean Time to Respond (MTTR): <4 hours
- Mean Time to Contain (MTTC): <24 hours
- Phishing click rate: <5%
- MFA adoption: 100% (SWIFT)
- Patch compliance: >95%
- Security training completion: 100%

**Operational KPIs:**
- System availability: >99.9%
- Backup success rate: 100%
- DR test success: 100%
- Incident escalation time: <30 min
- Change success rate: >95%
- Audit findings: 0 critical

**Compliance KPIs:**
- SWIFT CSCF compliance: 100%
- Policy compliance: >95%
- Access review completion: 100%
- Quarterly testing completion: 100%

**Trend Analysis:**
- Monthly comparison of all KPIs
- Quarterly trend reporting to executives
- Annual board presentation
- Continuous improvement targets

---

## Slide 48: Lessons Learned - What Went Wrong

**Critical Failures in Bangladesh Bank Heist:**

**1. The Printer Malfunction (Saved the Day):**
- Attackers' malware malfunctioned
- Complete printer failure = immediate red flag
- Detected within 90 minutes of Monday morning
- **$870 million saved by this failure**

**2. The "Fandation" Typo (Second Lucky Break):**
- Federal Reserve compliance officer noticed spelling error
- Enhanced scrutiny triggered
- **$20 million transfer blocked**

**3. Human Vigilance:**
- Bangladesh Bank operators immediately flagged silent printer
- Federal Reserve persistence in seeking confirmation
- Demonstrates importance of human review

**4. Physical Controls Matter:**
- Printer served as critical audit trail
- Low-tech safeguard caught high-tech attack
- Multiple control layers essential

**Key Insight:**
*"Defense in depth works. Multiple small controls can stop sophisticated attacks. Never underestimate the value of basic safeguards."*

---

## Slide 49: Lessons Learned - What We Must Remember

**Critical Takeaways for All Organizations:**

**1. No System is Immune:**
- Bangladesh Bank = Central Bank (high security expected)
- SWIFT network = "Secure" financial messaging
- Yet both were compromised at the endpoint
- Lesson: Endpoint security is paramount

**2. Detection > Prevention:**
- 10-month dwell time = prevention failed
- Detection capabilities saved the day (printer)
- Lesson: Assume breach, focus on detection

**3. Small Details Matter:**
- Spelling error stopped $20M
- Printer failure stopped $870M
- Lesson: Multiple control layers work

**4. Human Element is Critical:**
- Phishing started the attack
- Human vigilance stopped the attack
- Lesson: Training and awareness essential

**5. Time is Everything:**
- Weekend timing exploited by attackers
- 4-day window before detection intended
- Lesson: 24/7 operations and monitoring required

**6. Defense in Depth Works:**
- No single control would have stopped this
- Multiple failures enabled the attack
- Multiple safeguards ultimately limited damage
- Lesson: Layered security is non-negotiable

---

## Slide 50: Final Recommendations - Call to Action

**What Every Organization Must Do:**

**Immediate Actions (This Week):**
1. Assess your SWIFT/critical system security posture
2. Verify network segmentation exists
3. Enable MFA where possible immediately
4. Review and test emergency contact procedures
5. Conduct phishing awareness session

**Short-Term Actions (This Month):**
1. Perform gap analysis against SWIFT CSCF
2. Develop initial incident response plan
3. Establish 24/7 monitoring (even basic)
4. Review and update access controls
5. Begin security awareness training program

**Long-Term Actions (This Year):**
1. Implement comprehensive security program
2. Deploy detection and response capabilities
3. Establish continuous monitoring
4. Regular testing and exercises
5. Achieve compliance certifications

**Critical Questions to Ask:**
- Could this happen to us?
- How would we detect it?
- How quickly could we respond?
- Are we compliant with industry standards?
- Do our people know what to do?

**The Bottom Line:**
*"The Bangladesh Bank heist was preventable with proper controls. Learn from their mistakes. Invest in security now, or pay a catastrophic price later."*

---

## Slide 51: Questions & Discussion

**Discussion Topics:**

**For Policy/GRC Team:**
- Which policies should be our top priority?
- How do we ensure ongoing compliance?
- What governance structure is needed?

**For Technical/Software Dev Team:**
- What is the feasibility of network segmentation?
- Which technical controls are quick wins?
- What are the implementation challenges?

**For Operations Team:**
- How do we ensure 24/7 coverage?
- What operational changes are most critical?
- How do we balance security with productivity?

**For All Teams:**
- What are the biggest obstacles to implementation?
- How do we gain executive buy-in?
- What are the resource requirements?
- How do we measure success?

**Open Discussion:**
[Reserve time for team questions and cross-functional discussion]

---

## Slide 52: Conclusion & Next Steps

**Key Takeaways:**

1. **The Threat is Real:** Nation-state actors targeting financial institutions
2. **Prevention Alone is Insufficient:** Detection and response are critical
3. **Defense in Depth Works:** Multiple control layers saved $870 million
4. **Human Element Matters:** Training and vigilance are essential
5. **Compliance is Non-Negotiable:** SWIFT CSCF and industry standards required
6. **Investment Justifies ROI:** $10-15M investment to prevent $500M-1B+ loss

**Next Steps:**

**Week 1:**
- Consolidate team recommendations
- Prioritize quick wins
- Begin executive briefing preparation

**Week 2:**
- Present consolidated recommendations to leadership
- Request budget approval for Phase 1
- Assign implementation teams

**Week 3:**
- Begin immediate actions (MFA, monitoring)
- Develop detailed implementation plan
- Establish project governance

**Ongoing:**
- Regular progress reporting
- Continuous improvement
- Lessons learned integration

**Final Thought:**
*"In cybersecurity, the smallest oversight can lead to the largest losses—but also, the smallest safeguard can prevent catastrophe."*

**Thank you for your participation in this critical security exercise.**

---

## Appendix Slides (If Needed)

### Appendix A: Technical Architecture Diagrams
[Detailed network diagrams]

### Appendix B: Detailed Cost Breakdown
[Line-item budget estimates]

### Appendix C: SWIFT CSCF Control Mapping
[Full 31-control checklist]

### Appendix D: Incident Response Playbook Examples
[Detailed step-by-step procedures]

### Appendix E: Training Program Details
[Complete training curriculum]

### Appendix F: Metrics Dashboard Examples
[Sample KPI dashboards]

### Appendix G: Vendor Recommendations
[Specific product/service suggestions]

### Appendix H: References & Resources
[Citations, reports, further reading]

---

**END OF SLIDE DECK**

*This slide content is designed for educational purposes based on the Bangladesh Bank Heist case study. All recommendations are based on industry best practices and lessons learned from this incident.*
