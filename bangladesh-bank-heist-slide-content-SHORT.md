# Bangladesh Bank Heist 2016 - SHORT PRESENTATION (15 Minutes)

## PRESENTATION STRUCTURE
**Total Time: 15 minutes**
- Opening (All): 1 minute
- Policy/GRC Team: 3-4 minutes (3 slides)
- Technical/Software Dev Team: 3-4 minutes (3 slides)
- Operations Team: 3-4 minutes (3 slides)
- Consolidated Recommendations (All): 3-4 minutes (2-3 slides)

**Total Slides: ~12-14 slides maximum**

---

---

# OPENING SLIDES (1 minute - Presenter 1 or All Together)

---

## Slide 1: Title Slide
**Title:** Bangladesh Bank Heist 2016: Case Study Analysis

**Key Facts Box:**
- **Date:** February 4-5, 2016
- **Perpetrator:** Lazarus Group (North Korea)
- **Attempted:** $951 Million
- **Stolen:** $81 Million
- **Saved:** $870 Million (printer malware bug + typo)
- **Dwell Time:** 10 months undetected

---

## Slide 2: The Heist by Numbers

**What Happened:**

**💰 Financial Impact:**
- **$951M** - Total attempted theft
- **$870M** - Saved (malware bug + "Fandation" typo)
- **$81M** - Successfully stolen
- **$66M** - Still missing

**⏱️ Timeline:**
- **10 months** - Undetected in network
- **35 messages** - Fraudulent SWIFT transfers
- **90 minutes** - Discovery to investigation (Monday morning)

**🎯 The Ironic Twist:**
- Attacker's printer suppression malware **malfunctioned**
- Instead of hiding fraud prints → Stopped ALL printing
- Complete printer silence → Immediate red flag → $870M saved

**🔴 Critical Failures:**
- 0% MFA | 0 Network Segmentation | 0 SIEM | 0 IR Plan

---

---

# POLICY/GRC TEAM (3-4 minutes - 3 slides)

---

## Slide 3: Policy Failures - What Went Wrong

**Critical Policy Gaps:**

**1. Access Control ❌**
- No multi-factor authentication (MFA)
- Shared SWIFT operator credentials
- Weak passwords, no rotation
- No privileged access management

**2. Network Security ❌**
- SWIFT systems on corporate network
- No network segmentation
- No air-gapping requirements
- Internet/email access from SWIFT terminals

**3. Monitoring & Detection ❌**
- No 24/7 Security Operations Center
- No SIEM or centralized logging
- No intrusion detection systems
- No anomaly detection

**4. Incident Response ❌**
- No documented IR plan
- No emergency procedures
- Weekend coverage gaps exploited
- No security awareness training

**Result:** 10-month undetected presence, $951M theft attempt

---

## Slide 4: Policy Recommendations - Our Proposals

**Priority 1: Access Control**
- ✅ Mandatory MFA for ALL SWIFT access (hardware tokens)
- ✅ Privileged Access Management (PAM) solution
- ✅ Segregation of duties - dual approval >$1M
- ✅ 60-day credential rotation, no shared accounts

**Priority 2: Network Security**
- ✅ SWIFT network isolation (air-gap or strict segmentation)
- ✅ Zero-trust architecture
- ✅ No internet/email from SWIFT terminals
- ✅ Jump box with MFA for SWIFT access

**Priority 3: Monitoring & Detection**
- ✅ 24/7 SIEM monitoring with critical alerts
- ✅ Alert: After-hours SWIFT access → CRITICAL
- ✅ Alert: Transaction >$1M → HIGH (supervisor approval)
- ✅ Alert: **Printer failure >2 hours → HIGH**
- ✅ User Behavior Analytics (UEBA)

**Priority 4: Incident Response & Training**
- ✅ Documented IR plan with 24/7 procedures
- ✅ Monthly security awareness training
- ✅ Bi-weekly phishing simulations (Target: <5% click rate)
- ✅ Quarterly IR tabletop exercises

---

## Slide 5: Compliance Framework Alignment

**Industry Standards Implementation:**

**SWIFT Customer Security Controls Framework (CSCF):**
- ✅ All 31 mandatory controls
- ✅ Annual self-attestation
- ✅ Independent third-party assessment

**NIST Cybersecurity Framework:**
- ✅ IDENTIFY: Asset management, risk assessment
- ✅ PROTECT: Access control, awareness, segmentation
- ✅ DETECT: SIEM, IDS/IPS, continuous monitoring
- ✅ RESPOND: IR plan, 24/7 procedures
- ✅ RECOVER: DR testing, continuous improvement

**Key Policy Updates:**
- Annual policy reviews and updates
- Executive sponsorship and board oversight
- Regular compliance audits
- Metrics and KPIs for policy effectiveness

**Estimated Policy Implementation:** 3-6 months

---

---

# TECHNICAL/SOFTWARE DEV TEAM (3-4 minutes - 3 slides)

---

## Slide 6: Technical Failures - Attack Path

**How Attackers Exploited the Infrastructure:**

**The Vulnerable Architecture:**
```
Internet → Firewall → Corporate Network → SWIFT Network
           (Basic)    (Email/Workstations)  (No Isolation!)
                              ↓
                    DIRECT CONNECTION ❌
                    (No segmentation)
```

**Critical Technical Gaps:**

**1. Network Architecture ❌**
- No segmentation between corporate and SWIFT
- Flat network - phishing email → SWIFT access
- Single firewall, no defense-in-depth

**2. Endpoint Security ❌**
- Signature-based antivirus only (easily bypassed)
- No EDR, no application whitelisting
- Outdated/unpatched systems
- No email sandboxing

**3. Database Security ❌**
- No database activity monitoring
- evtdiag.exe malware injected into DB process
- Manipulated queries to hide fraudulent transactions

**4. Detection Systems ❌**
- No SIEM, no IDS/IPS, no UEBA
- 10-month dwell time undetected

---

## Slide 7: Technical Recommendations - Defense in Depth

**Proposed Security Architecture:**

**1. Network Segmentation (Priority 1)**
```
Internet → Perimeter FW → Corporate Network
                              ↓
                         ❌ NO PATH ❌
                              ↓
              Jump Box (MFA + Session Recording)
                              ↓
                         SWIFT Firewall
                              ↓
              ISOLATED SWIFT NETWORK
              - No internet/email access
              - Dedicated terminals only
```

**2. Endpoint Protection**
- ✅ Next-gen EDR (CrowdStrike, Carbon Black, SentinelOne)
- ✅ Application whitelisting (only approved apps run)
- ✅ Email security with sandboxing
- ✅ Patch management: Critical vulns <24 hours

**3. SWIFT-Specific Security**
- ✅ Latest SWIFT Alliance Access version
- ✅ Database Activity Monitoring (DAM)
- ✅ File Integrity Monitoring (FIM)
- ✅ **Redundant printers + automated health checks**
- ✅ Transaction anomaly detection

**4. Detection & Monitoring**
- ✅ Enterprise SIEM with 24/7 SOC
- ✅ Network IDS/IPS deployment
- ✅ UEBA for behavioral analysis
- ✅ Real-time threat intelligence

---

## Slide 8: Implementation Roadmap & Cost

**Phased Technical Implementation:**

**Phase 1: Critical (0-3 Months) - $2-3M**
- Deploy MFA for SWIFT (Immediate)
- Network segmentation (isolate SWIFT)
- Deploy EDR on all endpoints
- Basic SIEM with critical alerts
- Database activity monitoring
- PAM for privileged accounts

**Phase 2: High Priority (3-6 Months) - $3-5M**
- Full SIEM + 24/7 SOC
- Network IDS/IPS
- Email security gateway
- File integrity monitoring
- SWIFT software upgrades

**Phase 3: Enhancement (6-12 Months) - $2-3M**
- UEBA deployment
- Network traffic analysis
- IR automation (SOAR)
- Advanced threat intelligence

**Total Investment:** $8-13M over 12-24 months

**Key Metrics:**
- Mean Time to Detect (MTTD): <1 hour
- Mean Time to Respond (MTTR): <4 hours
- Phishing click rate: <5%
- System availability: >99.9%

---

---

# OPERATIONS TEAM (3-4 minutes - 3 slides)

---

## Slide 9: Operational Failures - What Broke Down

**Critical Operational Weaknesses:**

**1. Daily Operations ❌**
- No dual approval for high-value transactions
- Weekend/holiday monitoring gaps (exploited!)
- Manual reconciliation only (daily, not real-time)
- No automated transaction validation
- **Printer confirmations not reviewed regularly**

**2. Change Management ❌**
- No formal change approval process
- Malware installed undetected for 10 months
- No configuration baselines
- No testing environment for SWIFT changes

**3. Incident Response ❌**
- No documented IR procedures
- No 24/7 incident hotline
- Weekend timing exploited (bank closed Friday)
- Federal Reserve couldn't reach Bangladesh Bank
- No emergency contact procedures

**4. Training & Awareness ❌**
- Employees fell for phishing emails
- No regular security training
- SWIFT operators unaware of threats
- No incident reporting culture

**Impact:** Phishing succeeded, 10-month dwell time, delayed detection

---

## Slide 10: Operational Recommendations - Process Improvements

**Priority Operational Fixes:**

**1. Transaction Processing Controls**
- ✅ Dual approval for transactions >$500K
- ✅ Mandatory supervisor approval >$1M
- ✅ Real-time transaction validation and reconciliation
- ✅ Automated anomaly detection (volume, destination, timing)
- ✅ Daily balance verification with Federal Reserve

**2. 24/7 Operations**
- ✅ 24/7 SOC monitoring (in-house or outsourced)
- ✅ Weekend/holiday on-call rotation
- ✅ Emergency escalation procedures
- ✅ **Hourly printer health checks during business hours**
- ✅ Daily SWIFT system health verification

**3. Change Management**
- ✅ Formal change request and approval (CAB)
- ✅ Dedicated test environment for SWIFT
- ✅ Documented rollback procedures
- ✅ Quarterly privileged access reviews
- ✅ Automated deprovisioning

**4. Incident Response Procedures**
- ✅ 24/7 incident hotline established
- ✅ Documented IR playbooks for common scenarios
- ✅ 30-minute escalation to executives (critical incidents)
- ✅ Federal Reserve 24/7 contact established
- ✅ Quarterly IR tabletop exercises

---

## Slide 11: Training & Continuous Improvement

**Security Awareness Program:**

**Monthly Training Topics:**
- Phishing identification & reporting
- Social engineering tactics
- Password security & MFA
- Incident reporting procedures
- SWIFT-specific threats

**Phishing Simulation Program:**
- ✅ Bi-weekly random phishing tests
- ✅ Target: <5% click rate, >80% reporting rate
- ✅ Remedial training for failures
- ✅ Recognition for consistent reporters

**Regular Testing & Exercises:**

**Quarterly:**
- ✓ IR tabletop exercises
- ✓ Disaster recovery testing
- ✓ Emergency communication drills

**Semi-Annual:**
- ✓ Red team penetration testing
- ✓ Physical security audits
- ✓ Access reviews and recertification

**Annual:**
- ✓ Full-scale IR simulation
- ✓ Third-party security assessment
- ✓ SWIFT CSCF compliance audit

**Operational KPIs:**
- System availability: >99.9%
- Backup success rate: 100%
- Training completion: 100%
- Incident escalation time: <30 min

---

---

# CONSOLIDATED RECOMMENDATIONS (3-4 minutes - 2-3 slides)

---

## Slide 12: Implementation Priority Matrix

**What to Do First:**

**IMMEDIATE (0-30 Days) - Critical Security Gaps**
1. ✅ Deploy MFA for SWIFT access
2. ✅ Disable internet/email from SWIFT terminals
3. ✅ Establish 24/7 incident hotline
4. ✅ Create emergency contact list
5. ✅ Begin security awareness training

**HIGH PRIORITY (1-3 Months) - Major Vulnerabilities**
1. ✅ Network segmentation (isolate SWIFT)
2. ✅ Deploy EDR on all endpoints
3. ✅ Basic SIEM with critical alerts
4. ✅ Deploy PAM for privileged accounts
5. ✅ Formal change management process
6. ✅ Dual approval for high-value transactions

**MEDIUM PRIORITY (3-6 Months) - Strengthen Defenses**
1. ✅ Full SIEM + 24/7 SOC
2. ✅ Network IDS/IPS
3. ✅ Database activity monitoring
4. ✅ Email security gateway
5. ✅ IR playbook development and testing

**ONGOING (6-24 Months) - Maturity**
1. ✅ UEBA deployment
2. ✅ Advanced threat intelligence
3. ✅ SOAR automation
4. ✅ Compliance certifications (ISO 27001, SWIFT CSCF)
5. ✅ Regular red team exercises

---

## Slide 13: Cost vs. Risk - The Business Case

**Investment Required:**
- **Year 1:** $6-9M (infrastructure, tools, initial deployment)
- **Year 2:** $2-4M (completion, enhancements)
- **Ongoing Annual:** $3-5M (staff, licenses, SOC operations)

**Risk Mitigation:**
- **Bangladesh Bank Example:** $870M saved by malware bug
- **Actual Loss:** $81M stolen
- **Potential Loss (worst case):** $951M+

**ROI Calculation:**
- **Investment:** $10-15M over 2 years
- **Risk Prevented:** $500M-1B+ (potential future attacks)
- **ROI: 3,300% - 6,600%+**

**Intangible Benefits:**
- Reputation protection (priceless)
- Regulatory compliance (required)
- Customer confidence (competitive advantage)
- Operational resilience (business continuity)

**Cost of Inaction:**
- Potential complete loss of reserves
- Regulatory fines and sanctions
- Loss of international banking access
- Reputation damage (irreparable)
- Executive/board terminations

**Conclusion:** Security is not a cost—it's insurance against catastrophic loss.

---

## Slide 14: Key Takeaways & Lessons Learned

**What We Learned from Bangladesh Bank:**

**1. Small Details Can Save Millions**
- ✅ Attacker's printer malware bug → $870M saved
- ✅ "Fandation" spelling error → $20M blocked
- ✅ Federal Reserve vigilance → Stopped additional transfers
- **Lesson:** Defense in depth works. Multiple control layers matter.

**2. Detection > Prevention**
- ❌ 10-month dwell time = prevention failed
- ✅ 90-minute detection (printer) limited damage
- **Lesson:** Assume breach. Focus on rapid detection and response.

**3. Human Element is Critical**
- ❌ Phishing email started the attack
- ✅ Human vigilance (operators, Fed compliance officer) stopped it
- **Lesson:** Technology + trained people = effective defense

**4. Time is Everything**
- Attackers exploited weekend timing (Bangladesh + US weekends)
- 4-day detection window planned
- **Lesson:** 24/7 operations and monitoring are non-negotiable

**5. No Organization is Immune**
- Bangladesh Bank = Central Bank (high security expected)
- SWIFT network = "Secure" financial messaging
- Both compromised at the endpoint
- **Lesson:** If it can happen to them, it can happen to anyone

**Final Thought:**
> *"The smallest oversight can lead to the largest losses—but also, the smallest safeguard can prevent catastrophe."*

---

## Slide 15: Questions & Next Steps

**Critical Questions for Leadership:**

**Immediate:**
- Could this happen to us today?
- How would we detect it?
- Do we have 24/7 monitoring?
- Is SWIFT isolated from corporate network?
- Do we have an IR plan?

**Strategic:**
- Are we compliant with SWIFT CSCF?
- What's our current security posture?
- Do we have budget for critical controls?
- When can we start implementation?

**Next Steps:**

**This Week:**
- Consolidate team recommendations
- Prioritize quick wins (MFA, monitoring)
- Prepare executive briefing

**This Month:**
- Present to leadership for approval
- Request Phase 1 budget ($2-3M)
- Begin immediate actions

**This Quarter:**
- Implement critical controls
- Establish 24/7 monitoring
- Launch training program
- Quarterly progress reporting

**Thank you for participating in this critical security exercise.**

---

**END OF SHORT PRESENTATION**

---

## TIMING GUIDE FOR PRESENTERS

**Total: 15 minutes**

**Opening (1 min):**
- Slide 1: Title (15 sec)
- Slide 2: Numbers (45 sec)

**Policy/GRC Team (3-4 min):**
- Slide 3: Failures (1 min)
- Slide 4: Recommendations (1.5 min)
- Slide 5: Compliance (1 min)

**Technical/Software Dev Team (3-4 min):**
- Slide 6: Failures (1 min)
- Slide 7: Recommendations (1.5 min)
- Slide 8: Roadmap & Cost (1 min)

**Operations Team (3-4 min):**
- Slide 9: Failures (1 min)
- Slide 10: Recommendations (1.5 min)
- Slide 11: Training (1 min)

**Consolidated (3-4 min):**
- Slide 12: Priority Matrix (1 min)
- Slide 13: Cost vs Risk (1 min)
- Slide 14: Lessons Learned (1 min)
- Slide 15: Next Steps (30 sec)

**TOTAL: ~14-15 minutes**

---

## PRESENTATION TIPS

**For Each Team Member:**
- Stick to your allocated time (3-4 min max)
- Focus on 2-3 key points per slide
- Use the slides as visual aids, don't read them
- Practice your section at least once
- Have a backup if someone runs over

**Coordination:**
- Decide who presents which slide beforehand
- Have smooth transitions between team members
- Last person should bridge to next team

**Visual Tips:**
- Use ✅ ❌ symbols for quick visual impact
- Highlight key numbers in **bold** or color
- Keep bullet points short (max 5-7 words)
- Use the "$870M saved" as your hook

Good luck with your presentation! 🎯
