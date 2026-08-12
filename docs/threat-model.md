# Threat Model

## Purpose
The purpose of this threat model is to identify and evaluate relevant security threats to the password manager and the sensitive information it processes.

This document will catalogue the assets that require protection, the security assumptions and boundaries under which the system will operate, the threat actors considered and their capabilities, and the potential attack surfaces and threat scenarios affecting the system.

This document will be used to inform and refine security requirements, and guide architectural decisions, implementation choices, and testing throughout development.

This document is intended to be a living security artefact that may be updated as the system architecture and implementation introduce new security-relevant context.

## System Scope

The system consists of a locally operated desktop password manager application that shall store and manage a single user's sensitive information, primarily password-based credentials and secure notes.

**The system includes:**
- User authentication and vault unlocking.
- Creation and management of one or more independent local vaults.
- Storage, retrieval, and management of credentials and secure notes.
- Password generation and suitability evaluation.
- Vault import and export.
- Automatic vault locking.
- Audit and diagnostic logging.

**The system excludes:**
- Passkey management.
- Cloud synchronisation.
- Browser extensions.
- Mobile applications.
- Hardware security-key integration.

**External entities and interfaces:**
- The user.
- The host operating system and filesystem.
- Imported vault files entering the application.
- Exported vault files leaving the application.

**System states considered:**
- Application not running.
- Application running with no vault configured.
- Application running with an unavailable or invalid vault.
- Application running with a locked vault.
- Authentication in progress.
- Application running with an unlocked vault.
- Vault import and export in progress.

## Assets

### Credential Record
#### Description
A compound data record that associates an account or service with a username and a password.

#### Security Considerations
- Disclosure of the account or service could expose services on which the user has accounts. This could be used for targeted attacks such as phishing, typosquatting and website spoofing.

- Disclosure of the username could expose information about the user.

- Disclosure of the password could expose information about the user or allow account compromise.

- Modification to an individual credential field may prevent the user from accessing the associated account or service.

- Modification to multiple related fields could allow creation of a false but plausible credential record. Because the values remain internally consistent, the user is less likely to recognise that the stored credential has been tampered with.

Because of this it is important that not only each credential field be protected against unauthorised modification, but the association between them.


### Vault
#### Description
The vault is the protected collection of credential records, secure notes, security-related metadata, and information required by the application to maintain the stored data.

#### Security Considerations
- Disclosure of vault contents may expose multiple sensitive assets including credentials and secure note contents.

- Modification of the vault may alter, delete, replace, or inject stored information.

- Modification of the vault may affect the relationships between stored data resulting in apparently valid but untrustworthy records.

- Loss, deletion, or unrecoverable corruption of the vault could prevent the user from accessing the information stored inside, potentially denying the user the ability to access their accounts or services.

- Exported vault copies require equivalent protection to that of the active vault. This is because an exported copy may exist outside of the application's normal environment. An attacker in possession of an exported vault copy may attempt to compromise its protection offline via resources of their choosing.

- Imported vaults originate from outside of the application's current trusted state, thus they must be treated as potentially invalid, corrupted, or tampered with, until their validity and integrity have been established.


### Master Password / Authentication Secrets
#### Description
Secrets supplied by the user for authenticating to the system / unlocking the vault.

#### Security Considerations
- Disclosure of the master password or other authentication secrets could enable or materially assist unauthorised access to the vault.


### Cryptographic Key Material
#### Description
Keys or derived secrets used internally to protect vault contents.

#### Security Considerations
- Disclosure of key material could undermine confidentiality allowing partial or complete recovery of protected data.

- Modification or loss could make protected data inaccessible.


### Secure Notes
#### Description
The application allows users to store user-authored text notes as protected vault content.

#### Security Considerations
- Disclosure of information contained within a secure note has a security impact dependent on the sensitivity of the contents the user placed inside them. The application has no way to determine the sensitivity of each individual secure note and thus will need to treat all note contents as being potentially highly sensitive.

- Modification of secure notes may cause the user to trust incorrect information or may destroy information that cannot otherwise be recovered.


### Audit logs
#### Description
Records of significant system/security events during a session.

#### Security Considerations
- Disclosure of audit logs can expose sensitive information such as vault access times, usage patterns, and import/export activity.

- Modification of audit logs can obfuscate malicious actions taken during application sessions. This could hinder detection of suspicious activity and make reconstruction of the events timeline and resulting impact more difficult.


### Technical logs
#### Description
Diagnostic information generated by the application during operation, including runtime events, errors, and failures.

#### Security Considerations
- Disclosure of technical logs could expose sensitive data through exception messages, variable values, database errors, etc.

- Modification of technical logs could conceal application faults/failures or mislead troubleshooting efforts.


## Security Assumptions

### User
The user is assumed to have normal computer literacy but no specialist cybersecurity training.

The system shall not assume that the user can reliably recognise sophisticated malicious behaviour, social-engineering attempts, or deceptive content.

Therefore, expert user judgement shall not be relied upon as a primary security control.


### Host Hardware
The physical hardware and firmware of the host system are assumed to operate as intended and have not been maliciously modified or compromised.

Connected input, display, storage, and peripheral devices are assumed not to covertly capture, transmit, or manipulate sensitive application data. This assumption includes the absence of hardware or firmware-based keyloggers.

Defending against malicious hardware, compromised system firmware, or deliberate physical modification of the host environment is outside the scope of this threat model.

However, data received through otherwise trusted hardware, including imported vault files from removable storage, shall not be assumed to be trustworthy.


### Host Operating System
The host operating system is assumed to be a trusted execution platform whose normal security mechanisms are operating as intended.

A fully compromised host operating system is outside of the security guarantees of this application because the application cannot reliably protect sensitive data from an attacker with complete control over its execution environment.

The application shall still validate inputs and handle potentially corrupted or malicious data even when running on a trusted operating system.


### Other Local Software and Processes
Other software and processes running on the host are assumed not to maliciously observe, modify, or interfere with the password manager or its runtime data.

Defending against malicious software operating within the host environment is outside of the security guarantees of the application.

Data entering the application through defined interfaces shall still be treated as potentially malicious or corrupted.


### Application and Dependency Integrity
The application runtime, application code, and installed software dependencies are assumed not to have been maliciously modified or replaced.

Third-party dependencies are not assumed to be free from security vulnerabilities; however, they are assumed to be authentic versions of the dependencies intentionally selected by the project.

Defending against malicious replacement or modification of the application, its runtime, or its dependencies is outside the security guarantees of the application. This is because compromised executable code could bypass or alter security controls implemented by the system.

This trust does not extend to data processed by the application. Vault files and other external data shall not be assumed to have integrity by virtue of being accessed or parsed by the application.

### Publicly Known Application Information
The design and implementation of the application are not assume to be a secret. Threat actors may inspec the publicly visible version-control repository, including source code and project documentation.

The security of the system must therefore not rely on secrecy of its design or implementation.

## Threat Actors and Capabilities

### Local Person with Physical Access
#### Capabilities
- Can interact with the application through the local user interface.
- Can access files made available to the local user by the trusted host operating system and filesystem permissions.
- Can perform direct social engineering against the intended user.
- Can observe the user or display in an attempt to obtain authentication secrets, stored credentials, secure-note contents, or other sensitive information visible through the interface.
- Can steal host hardware ranging from the physical storage containing application data, to the entire host device.

#### Access Level / Preconditions
**Locked-vault state**
- Attacker can gain physical access to locked vault files.
- Attacker does not know authentication secrets.
- Access to protected vault functionality requires successful authentication.

**Unlocked-vault state**
- Attacker gains physical access after the legitimate user authenticates to the application, before automatic or manual locking occurs.
- Attacker can use protected vault functionality made available through the active unlocked application session, including creating, retrieving, updating, and deleting protected vault data. 

#### Limitations
- Attacker does not initially know the user's authentication secrets when considered in the locked-vault state.
- Cannot maliciously modify or control the trusted host hardware, firmware, operating system, application runtime, or application code.
- Cannot rely on malicious local software or processes to observe or interfere with the application.
- Cannot bypass application security controls by compromising components defined as part of the trusted execution environment.
- Physical possession of a copied or stolen locked vault does not itself grant access to its protected contents; subsequent offline analysis is modelled under the Opportunistic Attacker with Access to a Vault Copy profile.


### Opportunistic Attacker with Access to a Vault Copy
#### Capabilities
- Can retain, copy, inspect, and modify the acquired vault file.
- Can perform repeated offline analysis or attack attempts without the constraints of the application controls or authentication rate limits.
- Can use computing hardware, software tools, and storage under their own control.
- Can inspect publicly available application source code and documentation, and may understand the vault format and protection mechanisms used by the application.
- Can use the publicly available application to create arbitrary vaults containing attacker-selected data for comparison and analysis against the acquired protected vault.
- Can generate and repeatedly test arbitrary candidate authentication secrets against the acquired protected vault using publicly known application behaviours, formats, and security mechanisms.

#### Access Level / Preconditions
- Attacker has obtained a copy of a protected vault or protected vault export.
- Attacker does not have access to an authenticated application session.
- Attacker does not initially possess the user's authentication secrets.

#### Limitations
- Attacker does not control the user's trusted host environment or the application executing within it.
- Possession of the protected vault does not initially provide the attacker with its decrypted contents or the user's authentication secrets.


### Remote Attacker with User-Mediated Interaction
#### Capabilities
- Can communicate directly with the user.
- Can use social engineering to attempt to obtain the user's authentication secrets.
- Can use social engineering to attempt to induce the user to disclose sensitive information or perform security-relevant application actions.
- Can provide crafted or malicious vault files to the user and attempt to convince the user to import them into the application.
- Can attempt to persuade the user to disclose or transfer a protected vault/export to them. Once the attacker obtains the file, subsequent offline analysis is modelled under the Opportunistic Attacker with Access to a Vault Copy profile.

#### Access Level / Preconditions
- Attacker has a communication channel with the user.
- Attacker does not initially have physical or remote access to the application's host or the application executing inside it.

#### Limitations
- Attacker cannot directly interact with the application or its local interfaces. Application input from the attacker must cross the trust boundary through actions performed by the legitimate user.
- Attacker cannot directly access the host filesystem, application memory, or vault data.
- Attacker does not control trusted host components or local processes. If the attacker gains this level of control, the trusted execution environment has been compromised and the resulting scenario falls outside the security guarantees of the application.


## Attack Surfaces

## Threats

## Mitigations and Requirement Tracability

## Out-of-Scope Threats

## Open Security Questions