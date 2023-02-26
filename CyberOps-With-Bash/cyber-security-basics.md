# Cybersecurity Basics
:security:

Information commonly targeted by attackers includes personal communications (e-mail, text messages), pictures, trade secrets, payment information (credit/debit card numbers), personal identifiers (social security numbers), and sensitive government and military information.

Cybersecurity is a practice of protecting information and the systems that store or process information.

## 5 Principles of Cybersecurity

### Confidentiality

Information can be accessed and read only by authorized users.

Encryption and access control are typical mechanisms used to protect confidentiality.

### Integrity

Information can be modified only by authorized users.

Integrity should be easily verifiable.

Cryptographic hashing is often used to verify integrity of information.

### Availability

Information can be accessed when and where it is needed. Access should be timely and convenient for the user.

Redundancy, data and power backups, and failover sites are typically used to maintain high availability rates.

### Nonrepudiation

Nonrepudiation links an entity (user, program, etc.) to actions taken by that entity.

Common methods to ensure nonrepudiation include user authentication, digital signatures, and system logging.

### Authentication

Positively identifying and verifying the identity of a user. The success of the other 4 principles often depends on authentication.

Common mechanismsm used for authentication include usernames and passwords, electronic key cards, and biometrics.

## Attack Life Cycle

### 8 phases of the Attack Life Cycle model:

#### Reconnaissance

Attacker identifies the address space and layout of the target network, technologies in use, associated vulnerabilities, and information about the target organization’s users and hierarchy.

Passive Reconnaissance does *not* inject any data into or changes the target system. Ex: packet sniffing.

Active Reconnaissance does. Thus it is potentially detectable. Ex: port scanning.

#### Initial Exploitation

First action to gain access to a system, typically by exploiting a vulnerability in the system. Ex: SQL injection, brute-forcing.

This phase results in some level of access to the system.

#### Establish Foothold

Attacker ensures he can remain on the system for the long term and regain access as needed, since re-exploiting the system adds risk to the operation. Ex: creating new user, installing remote access trojan.

Permanence in this context is the ability to survive routine system maintenance (eg. reboots and patching).

This phase yields a permanent way to maintain a presence on the system and regain access as necessary.

#### Escalate Privileges

Often the initial level of access is not privileged enough to dump passwords or install software and accomplish whatever was the goal. Attacker would attempt to escalate privileges to a root or Admin account. Ex: buffer-overflow vulns, process injection, theft of creds.

Result of this phase is root or Admin access. Worse yet, this account would be usable acress systems on the network.

#### Internal Reconnaissance

With solidified foothold, attacker can begin to interrogate the network from the new vantage point inside the system.

Results of this phase is a more detailed map of the target network, hosts, and users, which will be used to refine the overall strategy and influence the next phase.

#### Lateral Movement

Movement across network to find the desired target system. Many attackers leave persistent backdoors on systems as they move laterally across the network.

#### Maintain Presence

As an alternative to persistent connection, so not to increase the chance of being detected, attackers have malicious implants periodically call back to a command-and-control server they operate. This is called beaconing.

#### Complete Mission

Collection and exfiltration of info from the target network. This is often masked as a normal traffic, using standard protocols and ports.

Or degradation of the system.
