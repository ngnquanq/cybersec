# Context and Definition
It is all about making sure the right people (identification and authentication) to use the right resources (authoriziation) and only those resources (least privilege principle). As the name is already imply, it is to answer question: Who are you and what you can do. 

In simple terms, it is having a security guard checking IDs and Keys and check if are you allow to go and use that specific resources and records everything that you are doing.  

IAM tools often add conviniences like SSO or MFA. 

For example, SSO lets user log in one and access many application without typing their passowrd again. MFA means requring two or more proffs (i.e password and a code sent to your phone), which make it harder for bad factors to fake. Using IAM corerctly can help org reduce the risk of breaches because users only get the access they need. 

In short, IAM is the framework of processes and technologies that manage digital identities and control user access so that only authorized people or devices can get to sensitive data. 

# Core IAM Components

## Identity Management Lifecycle
Identity management follows a lifecycle from creation to deletion:

**Provisioning:** Creating new user accounts and assigning initial access rights. This happens when someone joins the organization or changes roles.

**Maintenance:** Updating accounts as needs change (promotions, department transfers, additional access requests). Regular reviews ensure accounts stay current.

**Deprovisioning:** Removing or disabling accounts when no longer needed (employee leaves, contractor ends, role changes). Critical for security - orphaned accounts are a major risk.

**Identity Proofing:** Verifying someone is who they claim to be before creating credentials. May require multiple forms of ID, background checks, or in-person verification.

**Credential Management:** Issuing, resetting, and revoking passwords, tokens, certificates, and other authentication factors.

## Authentication Factors (The Five Types)

Authentication proves identity using one or more factors:

**Type 1 - Something You Know:**
- Passwords, PINs, passphrases
- Security questions
- Weakest alone but most common

**Type 2 - Something You Have:**
- Smart cards, tokens, key fobs
- Mobile devices (for push notifications or codes)
- Hardware security keys (YubiKey, etc.)

**Type 3 - Something You Are (Biometrics):**
- Fingerprints, iris/retina scans
- Facial recognition, voice recognition
- Cannot be reset if compromised
- Concerns: False acceptance rate (FAR) vs False rejection rate (FRR)
- Crossover error rate (CER): Where FAR = FRR, lower is better

**Type 4 - Somewhere You Are:**
- Location-based (GPS, IP address)
- Network location (internal vs external)

**Type 5 - Something You Do:**
- Typing patterns (keystroke dynamics)
- Signature dynamics
- Gait analysis

**Multi-Factor Authentication (MFA):** Combining two or more DIFFERENT types. Password + security question is NOT MFA (both Type 1).

## Access Control Models

Different approaches to managing who can access what:

**Discretionary Access Control (DAC):**
- Resource owners decide who gets access
- Flexible but less secure
- Example: File permissions in Windows/Linux where owner can share files
- Risk: Users may grant inappropriate access

**Mandatory Access Control (MAC):**
- System enforces access based on security labels/classifications
- Used in military and high-security environments
- Users cannot override (no discretion)
- Example: Top Secret, Secret, Confidential clearance levels
- Data labeled, users cleared, system enforces "no read up, no write down"

**Role-Based Access Control (RBAC):**
- Access based on job roles, not individuals
- Users assigned to roles, roles granted permissions
- Easier to manage at scale
- Example: "All accountants get access to financial systems"

**Attribute-Based Access Control (ABAC):**
- Access decisions based on attributes (user, resource, environment)
- Very flexible and granular
- Example: "Allow if user is in Finance AND accessing from corporate network AND during business hours"

**Rule-Based Access Control:**
- Access based on predefined rules
- Example: Firewall rules, time-of-day restrictions
- Often combined with other models

## Core IAM Principles

**Least Privilege:**
- Users get minimum access needed to do their job
- Default to deny, grant only what's necessary
- Reduces damage from compromised accounts
- Regular reviews to remove unneeded permissions

**Separation of Duties (SoD):**
- Split critical functions among multiple people
- No single person can complete a sensitive transaction alone
- Example: One person requests payment, another approves it
- Prevents fraud and errors

**Need to Know:**
- Access only to information required for specific tasks
- More restrictive than least privilege
- Common in classified/sensitive environments

**Privileged Access Management (PAM):**
- Special controls for admin/elevated accounts
- Check-out/check-in of privileged credentials
- Session recording and monitoring
- Time-limited access
- Example: Admin passwords stored in vault, checked out when needed

**Just-in-Time (JIT) Access:**
- Grant elevated permissions temporarily when needed
- Automatically revoked after time limit or task completion
- Reduces standing privileges
- Example: Approve 2-hour admin access for emergency patch

## Authentication Protocols and Technologies

**Kerberos:**
- Network authentication protocol using tickets
- Mutual authentication (both parties verify each other)
- Uses Key Distribution Center (KDC) with Authentication Server (AS) and Ticket Granting Server (TGS)
- Single sign-on capability
- Time-sensitive (requires synchronized clocks)

**LDAP (Lightweight Directory Access Protocol):**
- Protocol for accessing directory services
- Stores user accounts, groups, organizational structure
- Active Directory uses LDAP

**RADIUS (Remote Authentication Dial-In User Service):**
- Centralized AAA (Authentication, Authorization, Accounting)
- Client/server protocol
- Encrypts only the password
- Common for network access (WiFi, VPN)

**TACACS+ (Terminal Access Controller Access-Control System Plus):**
- Cisco's AAA protocol
- Encrypts entire authentication payload
- Separates authentication, authorization, and accounting
- More secure than RADIUS

**Federation (Identity Federation):**
- Trust relationship between organizations to share identity information
- Users authenticate once, access multiple systems across organizations
- Standards: SAML, OAuth 2.0, OpenID Connect

**SAML (Security Assertion Markup Language):**
- XML-based standard for exchanging authentication and authorization data
- Enables SSO across different domains
- Identity Provider (IdP) authenticates, Service Provider (SP) grants access

**OAuth 2.0:**
- Authorization framework (not authentication)
- Allows applications to access resources on behalf of user
- Example: "Sign in with Google" to access third-party app

**OpenID Connect:**
- Authentication layer built on OAuth 2.0
- Provides identity information about authenticated user

## Account Management

**Account Types:**
- **User accounts:** Standard accounts for individual employees
- **Privileged/Admin accounts:** Elevated permissions for system administration
- **Service accounts:** Used by applications and services (not humans)
- **Shared accounts:** Multiple users (high risk, avoid when possible)
- **Guest accounts:** Temporary access for visitors (should be heavily restricted)
- **Generic accounts:** Non-person accounts (risk: no accountability)

**Password Policies:**
- **Complexity requirements:** Mix of uppercase, lowercase, numbers, symbols
- **Minimum length:** Typically 12-16 characters for strong security
- **Password age:** Maximum time before forced change (balance security vs usability)
- **Password history:** Prevent reuse of recent passwords
- **Account lockout:** Temporarily disable after failed login attempts (prevents brute force)
- **Lockout duration:** How long account stays locked
- **Lockout threshold:** Number of failed attempts before lockout

**Account Monitoring:**
- Log and review authentication attempts (successful and failed)
- Track privileged account usage
- Alert on suspicious activity (impossible travel, unusual access times)
- Regular access reviews and recertification
- Identify dormant/unused accounts

**Access Recertification:**
- Periodic review of user access rights
- Managers confirm their team members still need current access
- Remove access no longer required
- Typically quarterly or annually depending on sensitivity

## Session Management

**Session Control:**
- Session tokens identify authenticated users
- Must be protected from theft (use HTTPS, secure cookies)
- Session timeout: Automatically log out after inactivity
- Absolute timeout: Maximum session length regardless of activity
- Concurrent session limits: Prevent account sharing

## Physical Access Controls

IAM isn't just digital - physical access matters too:

**Physical Authentication:**
- Badge readers (proximity cards, smart cards)
- Biometric readers at doors
- PIN pads
- Security guards checking ID

**Mantrap:**
- Small room with two doors
- First door locks before second opens
- Prevents tailgating (following someone through secure door)

**Tailgating vs Piggybacking:**
- Tailgating: Following without permission (unauthorized)
- Piggybacking: Following with permission (still violates security)

## Access Control Mechanisms

**Access Control Lists (ACLs):**
- List of permissions attached to resources
- Specifies which users/groups can access
- Common in file systems and networks

**Capabilities Tables:**
- List of resources each subject can access
- Opposite approach from ACLs (subject-focused vs object-focused)

**Context-Based Authentication:**
- Consider context: time, location, device, network
- Example: Require MFA if accessing from new device or location

**Adaptive/Risk-Based Authentication:**
- Adjust authentication requirements based on risk
- Low risk: password only
- High risk: MFA + additional verification
- Factors: unusual location, high-value transaction, sensitive data

## Security Threats and Concerns

**Identity Theft and Impersonation:**
- Attackers steal credentials to pose as legitimate users
- Mitigations: MFA, behavioral analysis, monitoring

**Credential Stuffing:**
- Using leaked username/password combinations from other breaches
- Users reuse passwords across sites
- Mitigations: MFA, password managers, breach monitoring

**Password Spraying:**
- Trying common passwords against many accounts
- Avoids account lockout (few attempts per account)
- Mitigations: Complex passwords, account monitoring, rate limiting

**Privilege Escalation:**
- Gaining higher access than authorized
- Vertical: User to admin
- Horizontal: Access another user's resources
- Mitigations: Least privilege, input validation, security updates

**Orphaned Accounts:**
- Accounts that remain active after user leaves or role changes
- High risk: No one monitoring, easy target for attackers
- Mitigations: Automated deprovisioning, regular access reviews

**Shared/Generic Account Risks:**
- No accountability (can't trace actions to individual)
- Difficult to revoke access when someone leaves
- Passwords shared insecurely
- Should avoid; if required, use strict controls and logging

**Social Engineering:**
- Manipulating people to give up credentials
- Phishing emails requesting passwords
- Pretexting (impersonating IT to request credentials)
- Mitigations: Security awareness training, MFA, verify requests

## Zero Trust Model

Modern approach: "Never trust, always verify"

**Principles:**
- Assume breach (network already compromised)
- Verify explicitly (authenticate and authorize every request)
- Least privilege access
- Micro-segmentation (limit lateral movement)
- Continuous monitoring and validation

**Implementation:**
- Identity is the new perimeter
- No automatic trust based on network location
- Strong authentication for all access
- Monitor all traffic and user behavior

# Case Studies: Real-World IAM Failures

## Case Study 1: Target Data Breach (2013)

**What Happened:**
In late 2013, Target suffered one of the largest retail breaches in history, compromising 40 million credit card numbers and 70 million customer records.

**IAM Failures:**
1. **Lack of Network Segmentation and Access Control:**
   - Attackers compromised a third-party HVAC vendor (Fazio Mechanical Services)
   - The vendor had network access to Target's systems for electronic billing and project management
   - This vendor account had excessive privileges - access beyond what was needed for their job function (violated Least Privilege)

2. **No Proper Privileged Access Management:**
   - The compromised vendor credentials allowed lateral movement across Target's network
   - Payment systems were accessible from the same network as vendor systems
   - No proper separation of duties or network segmentation

3. **Weak Third-Party Access Controls:**
   - Vendor used weak security practices (victim of phishing)
   - Target didn't enforce strong authentication requirements (no MFA) for third-party access
   - No monitoring of vendor account activities

**Impact:**
- $202 million in costs (after insurance)
- CIO and CEO resigned
- Multiple lawsuits and settlements
- Massive reputation damage

**What They Should Have Done:**
- Implement least privilege - vendor should only access billing systems, not POS network
- Require MFA for all vendor/remote access
- Network segmentation to isolate payment systems
- Continuous monitoring of privileged account activities
- Regular access reviews and recertification
- Zero Trust approach - verify every access request regardless of network location

## Case Study 2: Uber Data Breach (2016)

**What Happened:**
Hackers breached Uber's systems and stole personal information of 57 million riders and drivers. Uber then paid the hackers $100,000 to delete the data and kept the breach secret for a year.

**IAM Failures:**
1. **Exposed Credentials in Code:**
   - Engineers stored AWS credentials in code repositories on GitHub
   - Attackers found these credentials in a private GitHub repository
   - These were privileged credentials with access to sensitive data

2. **No Secrets Management:**
   - No vault or secrets management system for storing credentials
   - Credentials hardcoded instead of using secure credential management
   - No rotation of credentials

3. **Excessive Privileges:**
   - The compromised AWS credentials had access to production databases
   - Violated separation of duties - same credentials for dev and production
   - No just-in-time access or temporary credentials

4. **Lack of Monitoring:**
   - Unauthorized data access went undetected
   - No alerting on unusual database queries or data exports

**Impact:**
- $148 million in settlements with all 50 US states
- $1.17 million fine from UK regulators
- Chief Security Officer charged criminally for covering up the breach
- Severe reputation damage

**What They Should Have Done:**
- Implement proper secrets management (HashiCorp Vault, AWS Secrets Manager)
- Never store credentials in code repositories
- Use IAM roles with temporary credentials instead of static keys
- Implement PAM for privileged credentials with check-out/check-in
- Regular credential rotation
- Monitoring and alerting on database access patterns
- Principle of least privilege for all service accounts
- Separation of production and development credentials

## Case Study 3: Capital One Data Breach (2019)

**What Happened:**
A former AWS employee exploited a misconfigured web application firewall to steal data of 100 million Capital One customers and applicants.

**IAM Failures:**
1. **Overly Permissive IAM Roles:**
   - Web application had an IAM role with excessive permissions
   - Role could list and read S3 buckets it shouldn't access
   - Violated least privilege principle

2. **Server-Side Request Forgery (SSRF) Vulnerability:**
   - Firewall misconfiguration allowed attacker to access the metadata service
   - Retrieved IAM role credentials from the EC2 instance metadata
   - These credentials then used to access S3 buckets

3. **Insufficient Access Controls on Data:**
   - Sensitive data not properly segmented or restricted
   - Once inside with valid credentials, lateral movement was easy
   - No additional authorization checks on sensitive data buckets

4. **Lack of Monitoring and Alerting:**
   - Unusual S3 access patterns not detected quickly enough
   - No real-time alerting on large data exports
   - Breach went undetected for months

**Impact:**
- $80 million fine from OCC (Office of the Comptroller of the Currency)
- $100-150 million settlement for affected customers
- Significant remediation costs
- Reputation damage

**What They Should Have Done:**
- Implement least privilege IAM policies (only access specific required buckets)
- Use IAM policy conditions to restrict access by IP, time, or other factors
- Regular IAM policy audits and automated compliance checking
- Properly configure WAF to prevent SSRF attacks
- Implement defense in depth - even with credentials, shouldn't access everything
- Use S3 bucket policies as additional layer of access control
- Implement CloudTrail logging and real-time monitoring for unusual API calls
- Set up alerts for bulk data access or exports
- Regular security assessments and penetration testing

## Case Study 4: SolarWinds Supply Chain Attack (2020)

**What Happened:**
Russian state-sponsored hackers compromised SolarWinds' Orion platform, inserting malware into software updates that were then distributed to approximately 18,000 customers, including US government agencies and Fortune 500 companies.

**IAM Failures:**
1. **Weak Password on Critical Systems:**
   - SolarWinds used "solarwinds123" as password for update server
   - Found publicly exposed on GitHub
   - No password complexity requirements enforced

2. **Lack of MFA:**
   - Critical build systems didn't require multi-factor authentication
   - Single factor (weak password) was enough to access build pipeline

3. **No Privileged Access Management:**
   - No proper controls on who could access build systems
   - No session recording or monitoring of build server access
   - Standing privileges instead of just-in-time access

4. **Insufficient Access Monitoring:**
   - Unauthorized access to build systems went undetected
   - Malicious code injected without triggering alerts
   - No code review or change approval process with proper separation of duties

5. **VPN Access Without MFA:**
   - Remote access to internal systems didn't require MFA
   - Once attackers had credentials, they had broad access

**Impact:**
- Affected 9 US federal agencies including Treasury, Justice, State, Homeland Security
- Thousands of private sector organizations compromised
- Considered one of the most sophisticated and damaging cyberattacks in history
- Estimated costs in billions across all affected organizations
- SolarWinds paid settlements and faced lawsuits

**What They Should Have Done:**
- Enforce strong password policies (complexity, length, no common passwords)
- Require MFA for all access, especially privileged/critical systems
- Implement PAM with just-in-time access for build systems
- Session recording and monitoring for all privileged activities
- Separation of duties in build pipeline (code review, approval workflow)
- Code signing and integrity verification
- Network segmentation to limit access to build environment
- Regular security audits of access controls
- Automated detection of credential exposure (scan GitHub, etc.)
- Zero Trust architecture - don't trust internal network

## Case Study 5: Twitter Internal Tools Breach (2020)

**What Happened:**
Attackers used social engineering to compromise Twitter employee credentials, gaining access to internal admin tools. They hijacked high-profile accounts (Barack Obama, Elon Musk, Bill Gates, etc.) to promote a Bitcoin scam.

**IAM Failures:**
1. **Social Engineering Success:**
   - Attackers called Twitter employees pretending to be IT support
   - Successfully obtained credentials from multiple employees
   - No verification process for password reset requests

2. **Excessive Admin Tool Access:**
   - Too many employees had access to powerful internal admin tools
   - These tools could take over any user account
   - Violated least privilege - not all support staff needed this level of access

3. **Insufficient MFA:**
   - While some systems had MFA, internal admin tools may not have required it for all actions
   - MFA bypass possible through social engineering

4. **No Just-in-Time Access:**
   - Standing privileges to admin tools rather than temporary access when needed
   - No approval workflow for using powerful account takeover features

5. **Weak Separation of Duties:**
   - Single employees could perform high-risk actions without approval
   - No dual control or maker-checker process for sensitive operations

**Impact:**
- Major embarrassment for high-profile users
- Over $100,000 in Bitcoin stolen from scam victims
- FTC settlement and security improvements mandated
- Loss of user trust
- Multiple employees terminated

**What They Should Have Done:**
- Comprehensive security awareness training to prevent social engineering
- Out-of-band verification for password resets (not via phone to unverified caller)
- Implement least privilege - limit who has access to account takeover tools
- Require strong MFA that's resistant to social engineering (hardware keys, not SMS)
- Just-in-time privileged access - grant admin rights only when needed, time-limited
- Implement separation of duties for high-risk actions (require two people)
- Extensive logging and real-time monitoring of admin tool usage
- Alert on unusual patterns (multiple account accesses in short time)
- Regular recertification of who needs access to internal tools

## Common Themes Across All Cases

**Recurring IAM Failures:**
1. **Violation of Least Privilege** - Users/systems had more access than needed
2. **Lack of MFA** - Relying on passwords alone
3. **Poor Credential Management** - Hardcoded, weak, or exposed credentials
4. **Insufficient Monitoring** - Breaches went undetected for extended periods
5. **No Privileged Access Management** - Uncontrolled admin access
6. **Weak Third-Party Access Controls** - External vendors not properly restricted
7. **Missing Separation of Duties** - Single points of failure in security
8. **No Network Segmentation** - Lateral movement too easy once inside

**Key Lessons:**
- IAM is not just about authentication - it's about the entire lifecycle of identity and access
- Defense in depth: Multiple layers of controls, so one failure doesn't compromise everything
- Zero Trust: Verify every access attempt, regardless of where it originates
- Continuous monitoring and rapid response are critical
- Regular audits and access reviews catch privilege creep and orphaned accounts
- Security awareness training reduces social engineering success
- Third-party access is as important as employee access

# Case Study