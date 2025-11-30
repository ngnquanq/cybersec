# Bangladesh Bank Cyber-Heist: Timeline and Methodology

## Overview

The cyber-heist perpetrated against Bangladesh Bank (BB) in February 2016 was a central event in a multi-year conspiracy that involved computer intrusions, data theft, and financial fraud. The attack resulted in the largest successful cyber-theft from a financial institution to date.

---

## What Happened

The attack resulted in a successful loss of approximately **$81 million**. The overall operation at Bangladesh Bank involved an attempted theft that approached $1 billion, which contributes to the attempted losses of well over $1 billion across all financial services victims targeted by this group.

The funds were successfully routed to accounts in the Philippines, while an additional $20 million routed to an account in Sri Lanka was stopped by the recipient bank before reaching its intended destination. The funds successfully stolen were subsequently laundered through multiple bank accounts, a money remitting business, and casino junkets.

---

## Exact Timestamps and Chronology

The planning and execution of the attack occurred over more than a year:

| Date/Timeframe | Event | Source |
|----------------|-------|--------|
| **October 7-8, 2014** | Subjects began online reconnaissance targeting specific banks in Bangladesh, including Bangladesh Bank | - |
| **January 29 - February 24, 2015** | At least three Bangladesh Bank computers successfully downloaded the malicious payload contained in the spear-phishing emails | [164.a] |
| **January 29, 2016** | The subjects performed lateral movements throughout the network, accessing Bangladesh Bank's SWIFTLIVE system | [164.c] |
| **February 2016** | The hackers executed the fraudulent transfers | - |
| **February 6, 2016 at 6:00 AM (local time)** | Malware (evtdiag.exe) was scheduled to instruct another malware file (evtsys.exe) to securely delete itself | - |

---

## How They Did It (Methodology)

The attack involved multiple phases, starting with targeted deception and culminating in surgical manipulation of critical financial infrastructure:

### 1. Initial Access and Infection (Spear-Phishing)

The intrusion began with reconnaissance and social engineering techniques:

- **Reconnaissance**: Subjects researched the bank and its employees prior to the intrusion.

- **Spear-Phishing**: Emails, tailored to appear legitimate and sometimes purporting to be requests for employment, were sent to employees. These messages included a link purporting to contain a résumé and cover letter (e.g., to a file named `Resum.zip`). The successful download of the malware payload indicates that the bank's email filtering, gateway security, and user defenses failed.

### 2. Network Penetration and Evasion

Once inside the network, the attackers utilized sophisticated tools to move laterally and hide their communications:

- **Malware Deployment**: The attackers deployed malware families, including:
  - **NESTEGG**: A memory-resident backdoor [170.b, 250, 622]
  - **MACKTRUCK**: Multiple variants [170.c, 254, 622]

- **Evasion**: NESTEGG was designed to run in the computer's memory without residing on the hard drive, making it difficult for traditional anti-virus software to detect [170.b, 250, 622].

- **FakeTLS Protocol**: The attackers used a custom communication protocol called FakeTLS (Transport Layer Security) that mimicked authentic encrypted TLS traffic but used a different encryption method. This allowed communications to proceed without triggering security alerts in systems designed to ignore encrypted traffic.

### 3. Execution of the Theft

The attackers pivoted to the bank's most critical asset, the SWIFT system:

- **Lateral Movement**: The subjects moved through the internal network to access the computer terminals interfacing with the SWIFT communication system (SWIFTLIVE) [164.c, 623].

- **Impersonation**: With access to the SWIFT system, they gained sufficient privileges to impersonate authorized bank employees.

- **Fraudulent Messages**: They crafted and sent fraudulent but authenticated SWIFT messages that directed the Federal Reserve Bank of New York (FRBNY) to transfer funds from Bangladesh Bank's account to specified accounts in the Philippines and Sri Lanka.

### 4. Evidence Elimination (Cover-Up)

The subjects implemented specific coding to eliminate forensic artifacts:

- **Transaction Record Deletion**: Malware named `evtdiag.exe` was deployed to access the database storing SWIFT message records and delete the specific messages that instructed the fraudulent transactions, effectively covering the subjects' tracks [179.b.ii, 275, 624].

- **Printout Modification**: Malware named `nroff.exe` was used to intercept and modify fraudulent transactions that would have otherwise been automatically printed for the bank's records.

- **Secure Malware Deletion**: The subjects ensured their malware was nearly impossible to recover by using a unique "secure delete" function that:
  - Generated random data to over-write the part of the hard drive allocated to store the file
  - Renamed the file
  - Performed a regular Windows deletion [179.b.i, 274]
  - NESTEGG also securely erased itself from the hard drive after running in memory

---

## Key Takeaways

- **Multi-year operation**: Attack planning began as early as October 2014
- **Sophisticated malware**: Memory-resident backdoors and custom encryption protocols
- **Critical system compromise**: Direct access to SWIFT terminals
- **Evidence destruction**: Systematic elimination of forensic artifacts
- **Massive financial impact**: $81 million successfully stolen, nearly $1 billion attempted
