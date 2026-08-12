# Decision Log
This log records significant project, technology, process, and engineering decisions. Detailed architecture decisions will be added as architectural design progresses.

Historical decisions recorded before adoption of dated decision logging do not include decision dates. New decisions will include the date on which they were accepted.


## DEC-001: Use Python 3.x as the implementation language
**Status:** Accepted

### Context
The project requires a language suitable for desktop application development, database interaction, automated testing and security libraries.

### Decision
Python 3.x will be used as the primary implementation language

### Rationale
I have previous Python experience which will speed up development time and effort. This will allow more time spent on software engineering, security, and architecture.

### Alternatives Considered
None formally considered.

### Consequences
- Access to the Python ecosystem and standard library
- Runtime and memory-management characteristics of Python must be considered when dealing with sensitive data.


## DEC-002: Use Tkinter for GUI
**Status:** Accepted

### Context
The project will require a GUI.

### Decision
Tkinter will be used for the GUI.

### Rationale
Tkinter is a lightweight framework that is included with Python.

### Alternatives Considered
None formally considered.

### Consequences
Some time will need to be spent familiarising with this framework.


## DEC-003: Use SQLite for local persistence
**Status:** Accepted

### Context
The system will require a way to both store and search through vault data

### Decision
SQLite will be used as a backend database

### Rationale
SQLite is appropriate for a standalone desktop application. It is lightweight and does not require any external database services.

### Alternatives Considered
MySQL

### Consequences
Some time will need to be spent re-familiarising myself with SQL and database architecture.


## DEC-004: Use pytest for automated testing
**Status:** Accepted

### Context
The codebase will require unit tests to ensure intended behaviour

### Decision
pytest will be used for automated unit testing

### Rationale
pytest is a Python-native testing framework that is compatible with the intended TDD/unit testing workflow.

### Alternatives Considered
None formally considered.

### Consequences
Some time will need to be spent familiarising myself with the pytest framework.


## DEC-005: Use Git/GitHub for version control
**Status:** Accepted

### Context
The project will need version control.

### Decision
Git/GitHub will be used as the version control.

### Rationale
Provides revision history and allows the development process to be demonstrated to potential employers.

### Alternatives Considered
None formally considered.

### Consequences
Development practices must include regular commits/pushes and repository hygiene.


## DEC-006: Use VS Code for development environment
**Status:** Accepted

### Context
The project needs a development environment

### Decision
VS Code will be used as the development environment.

### Rationale
VS Code has integration for Python, Markdown, Git and terminal workflows in a single environment.

### Alternatives Considered
PyCharm
Eclipse

### Consequences
Project setup may include editor specific local configuration, which should not become a dependency for building/running the application.


## DEC-007: Use project-local .venv virtual environment
**Status:** Accepted

### Context
The coding environment will need to be set up for Python development.

### Decision
A local virtual environment will be used inside VS Code for code development.

### Rationale
This will keep dependencies isolated to the project and help ensure reproducible setup.

### Alternatives Considered
Use system Python installation

### Consequences
Ensure .gitignore updated to exclude virtual environment files that will be created.


## DEC-008: Make the project repo public
**Status:** Accepted

### Context
A decision needed to be made to either have the repository publicly visible or kept private.

### Decision
Repository to be publicly visible

### Rationale
The project is intended as a portfolio piece whose code, tests, documentation and development history is intended to be inspected. It also allows demonstration of good sanitisation practice when dealing with security sensitive application development.

### Alternatives Considered
Private visibility.

### Consequences
It is important that any sensitive information and test data containing sensitive information is kept from being exposed in the public repository.
A well-crafted .gitignore is paramount.


## DEC-009: Release project under MIT License
**Status:** Accepted

### Context
As part of using Git/GitHub for version control, a license type is requested for the project.

### Decision
Release project under MIT License

### Rationale
MIT License is a simple, permissive and widely recognised open-source license that is appropriate for a portfolio project.

### Alternatives Considered
None formally considered.

### Consequences
Third parties may reuse, modify, and redistribute the software subject to the license terms.


## DEC-010: Limit initial credential type to password-based credentials
**Status:** Accepted

### Context
A decision had to be made regarding the scope of credential types the vault will support.

### Decision
The initial project will support password-based credentials containing an account/service identifier, username, and password.

### Rationale
This will keep the project achievable within a reasonable timeframe while leaving the possibility of supporting additional credential types in future versions.

### Alternatives Considered
Passkeys
WebAuthn/hardware-backed credentials

### Consequences
This will limit the functionality of project's initial release. However it will make the project more manageable in terms of scope and time to completion.

The system should be designed with future credential types in mind without implementing support for them prematurely.


## DEC-011: Scope Boundaries
**Status:** Accepted

### Context
Decisions had to be made about what capabilities and functionality the project deliverable will achieve.

### Decision
Exclude passkeys, Webauthn, hardware keys, cloud synchronisation, browser integration and mobile applications from the current scope.

### Rationale
This will keep the project scope manageable, prevent scope creep, and allow the project to be completed in a reasonable timeframe.

### Alternatives Considered
None formally considered.

### Consequences
Limitations to feature development


## DEC-012: Add secure notes as a data type
**Status:** Accepted

### Context
The ability for the vault to store secure notes would be desirable.

### Decision
Secure notes will be an included sensitive-data type the vault can store.

### Rationale
This functionality is both useful and tests the code's extensibility beyond just username:password credentials without greatly expanding the project scope.

### Alternatives Considered
None formally considered.

### Consequences
Project architecture and security considerations will need to cover this proposed functionality.


## DEC-013: Minimum Viable Product approach
**Status:** Accepted

### Context
A decision had to be made on the milestones for the project.

### Decision
An MVP version of the project has been decided with later versions building on this foundation.

### Rationale
This will prioritise completion of a small core system before adding additional functionality and quality of life updates.

### Alternatives Considered
None formally considered.

### Consequences
The project will use an iterative and incremental delivery approach, with each version building on the previous milestone.


## DEC-014: Continuous development strategy
**Status:** Accepted

### Context
A decision had to be made on how documentation and testing is to be treated during the project.

### Decision
Testing and documentation will be treated as continuous development activities.

### Rationale
This will reduce the risk of system regression and will keep documentation aligned with implementation.

### Alternatives Considered
Treat testing and documentation as final milestones

### Consequences
Testing and documentation will become living artifacts that will need regularly updating throughout the project.


## DEC-015: Separate the original project proposal
**Status:** Accepted

### Context
The original project proposal was written at the very beginning of this project journey.

### Decision
Keep the proposal as it forms a solid foundation for the project; create the living engineering documents requirements, architecture, threat model etc in markdown and use proposal contents to help create the initial drafts.

### Rationale
This will make use of work already carried out in the proposal whilst creating a better document structure to facilitate DEC-014.

### Alternatives Considered
None formally considered.

### Consequences
Some time will be required to create the new document structure and transpose the work carried out in the project proposal.


## DEC-016: Separate requirements from implementation decisions
**Status:** Accepted

### Context
Whilst in the planning phase there will be decisions and documents made regarding requirements, implementation, and architecture aspects of the project.

### Decision
Keep a clear separation between these concepts when planning for the project.

### Rationale
Requirements describe security and environmental restrictions, and behaviours; architecture and design documents describe how these will be achieved.

### Alternatives Considered
None formally considered.

### Consequences
Care has to be taken when filling out the requirements document to ensure that it does not imply or take on an implementation approach.


## DEC-017: Separate functional requirements for vault import and export
**Status:** Accepted

### Context
The project has functional requirements for the importing and exporting of vaults.

### Decision
Keep these two functionalities separated.

### Rationale
Although they are both involved with the same functional area of the application, they are independently concerned with different aspects of that functionality.
Keeping them separated makes testing clearer as they are both separate failure points.

### Alternatives Considered
None formally considered.

### Consequences
This will shape some implementation and code design choices during those planning phases.


## DEC-018: Categorise protection of vault data at rest as a non-functional security requirement.
**Status:** Accepted

### Context
This was originally categorised as a vault functional requirement.

### Decision
Move this requirement to non-functional security.

### Rationale
This is a security quality/property of the vault rather than an operational function.

### Alternatives Considered
None formally considered.

### Consequences
Slight change to the requirements document. This may change what/how some tests are written during code development.


## DEC-019: Separate audit logging from diagnostic/application logging
**Status:** Accepted

### Context
The project requires both audit information about significant application actions and diagnostic logging to support troubleshooting.

### Decision
Separate these two logs.

### Rationale
Audit records describe significant user/system actions, while diagnostic logs describe application behaviour and failures. They have different purposes that have different security considerations.

### Alternatives Considered
None formally considered.

### Consequences
This will affect some implementation and design choices at that stage of the project.


## DEC-020: Do not reject passwords that fail suitability checks
**Status:** Accepted

### Context
There is a choice to be made if password strength rules should be suggested or enforced.

### Decision
The rules should only be suggestions.

### Rationale
Password strength functionality should provide guidance rather than prevent users from storing the credentials they choose. Strict adherence could also cause issues if the user migrating to this system has previous passwords that violate any of the defined rules.

### Alternatives Considered
None formally considered.

### Consequences
This will have an impact on the system's design/implementation when at that stage of the project.


## DEC-021: Automatic vault locking is mandatory.
**Status:** Accepted

### Context
The system will have functionality that allows the vault to be locked after a period of inactivity.

### Decision
Automatic vault locking will be mandatory. A user-configurable inactivity timout will be treated as an optional convenience feature and is not part of the MVP.

### Rationale
This is a baseline level of security.

### Alternatives Considered
None formally considered.

### Consequences
This will shape some of the system design choices.


## DEC-022: The performance test vault will contain 300 credentials
**Status:** Accepted

### Context
For performance testing, a decision has to be made as to how many credentials will be in the vault at the time of the tests.

### Decision
The vault will have 300 credentials. 

### Rationale
This will be representative of a conservative above-average workload, this is not intended as an arbitrary maximum credential count.

### Alternatives Considered
Possibly running tests with a 1,000 credential vault in parallel as a stress test.

### Consequences
A vault containing 300 test credentials will need to be generated and stored for testing purposes.


## DEC-023: Use defined reference workload and hardware
**Status:** Accepted

### Context
Performance tests will need to be measured against some metrics.

### Decision
To carry out performance tests the project will use a defined hardware and workload.

### Rationale
This makes the requirements measurable and defensible rather than using vague metrics like 'low-end hardware'.

### Alternatives Considered
subjective metrics.
qualitative metrics.

### Consequences
Suitable metrics will need to be decided upon with concrete rationale.


## DEC-024: Keep system architecture modular and decoupled.
**Status:** Accepted

### Context
Some requirements raised questions about the extensibility and responsibilities of areas of the codebase.

### Decision
Make sure the codebase's architecture is modular and realistically decoupled.

### Rationale
This decision will help shape the architectural decision making without prescribing any specific design choices at this stage.

### Alternatives Considered
None formally considered

### Consequences
This decision establishes an architectural principle without prescribing any specific patterns or component boundaries before the architecture phase.


## DEC-025: Each vault will support a single user
**Status:** Accepted
**Date:** 11/08/2026

### Context
A decision was required regarding whether an individual vault should support access by multiple users.

### Decision
Each vault will support a single user and a single associated authentication context. A single user may create or use multiple separate vaults.

Multi-user vault access will not be supported within the scope of this project but may be considered as a future feature.

### Rationale
Supporting multiple users within a single vault would introduce additional authentication, authorisation, access-control, and data ownership requirements.

Restricting each vault to a single user keeps the security model and project scope manageable while still allowing users to maintain separate vaults for different contexts.

### Alternatives Considered
Multiple users sharing a single vault.
Multiple users with different permissions within a vault.
Restricting each user to a single vault.

### Consequences
The application will not need to implement per-user authorisation or permissions within a vault.

A vault cannot be shared between multiple users while maintaining separate identities or permissions.

Authentication and vault-unlocking functionality can assume a single-user security context.

A single user may maintain multiple independent vaults.


## DEC-026: Treat the host operating system as a trusted platform
**Status:** Accepted
**Date:** 11/08/2026

### Context
The password manager depends on the host operating system for process isolation, memory management, filesystem access, user input, and other runtime services.

A decision was required regarding whether the threat model should attempt to defend against a maliciously compromised host operating system.

### Decision
The application will assume that the host operating system is not maliciously compromised and that its normal security mechanisms are operating as intended.

A fully compromised host operating system will be treated as outside the security guarantees of the application.

### Rationale
The security of the host operating environment is outside the application's direct control. A fully compromised operating system can undermine protections implemented by the application; therefore, defending against a fully compromised host operating system is outside the scope of this threat model.

### Alternatives Considered
Treat the host operating system as potentially malicious or fully compromised.

### Consequences
If the host operating system is compromised, the confidentiality, integrity, and availability guarantees provided by the password manager may no longer hold.

The application should still validate external inputs and handle potentially corrupted or malicious data even when operating on a trusted host operating system.


## DEC-027: Trust host hardware and firmware
**Status:** Accepted
**Date:** 12/08/2026

### Context
The password manager depends on the host hardware and firmware for a working environment on which it is to operate.

A decision was required regarding whether the threat model should attempt to defend against malicious modification of or tampering with the host hardware or firmware.

### Decision
The system will assume that the host hardware and firmware is not maliciously compromised and that the host hardware and firmware are assumed to opeate as intended.

Compromised host hardware and firmware will be treated as outside the security guarantees of the application.

### Rationale
The security of the host hardware and firmware is outside the application's direct control. The system requires a trusted execution foundation and cannot realistically establish security guarantees against malicious hardware and firmware controlling that foundation. Therefore, defending against such attacks is outside the scope of this threat model.

### Alternatives Considered
Treat the host hardware and firmware as potentially malicious or fully compromised.

### Consequences
If the host hardware and firmware is compromised, the confidentiality, integrity, and availability guarantees provided by the password manager may no longer hold.

This constraint does not consider stolen or copied storage data as out of scope.

The application should still validate inputs and handle potentially corrupted or malicious data even when operating within a trusted host environment.


## DEC-028: Exclude malicious local software/processes from threat model
**Status:** Accepted
**Date:** 12/08/2026

### Context
The application will be running in an environment where other software/processes will be executing.

A decision was required regarding whether the threat model should attempt to defend against potentially malicious behaviour from these other software and processes sharing the local execution environmnet.

### Decision
The system will assume that other software/processes executing in the same environment do not maliciously obseve, modify, or interfere with the password manager or its runtime data.

Maliciously acting software/processes will be treated as outside the security guarantees of the application.

However, data entering through application interfaces will remain untrusted.

### Rationale
The behaviours of other software and processes are outside the application's direct control. Software executing with sufficient access to observe, modify, or interfere with the application's runtime could bypass protections from outside the application's own control boundary. Requiring the application to remain secure within an actively hostile local execution environment would therefore substantially expand the system's security model and is outside the scope of this threat model.

### Alternatives Considered
Treat the executing environment as shared by hostile software/processes.

### Consequences
If there are maliciously acting software/processes executing in the same environment, the confidentiality, integrity, and availability guarantees provided by the password manager may no longer hold.

This constraint does not consider malicious or corrupted data entering through defined application interfaces, including vault import functionality, to be out of scope.


## DEC-029: Trust application/runtime/dependency integrity
**Status:** Accepted
**Date:** 12/08/2026

### Context
The system depends on application code written as part of the project, libraries developed by third parties, and a runtime environment that enables the intended system behaviours.

A decision was required regarding whether the threat model should attempt to defend against potentially malicious tampering with these components of the system.

### Decision
The application code is assumed not to have been maliciously modified or replaced.

The Python runtime is assumed to be authentic and not maliciously modified.

Software dependencies are assumed to be authentic versions intentionally selected by the project. However, they are not assumed to be free from vulnerabilities.

Therefore malicious modification or replacement of application code, runtime, or dependencies is considered outside the security guarantees of the system.

### Rationale
The application code, runtime, and selected dependencies form the trusted execution foundation upon which the application's security controls depend.

The application cannot reliably guarantee its own security if components responsible for implementing or verifying those controls are themselves compromised. Self-verifying mechanisms will ultimately depend on some trusted verification mechanism or value that an attacker cannot modify alongside the application.

Therefore, malicious compromise of the trusted execution foundation will be treated as outside the application's security guarantees.

This does not rule out the implementation of integrity or authenticity checks as a defence-in-depth measure to detect modification before a session is launched. Such measures would reduce reliance on this assumption but would not remove the need for an underlying trusted foundation.

### Alternatives Considered
Treat application code, the runtime, and dependencies as potentially maliciously modified or replaced.

### Consequences
Security guarantees depend on the application executing with an authentic and untampered application codebase, runtime, and set of intended dependencies.

Malicious replacement or modification of these components will not be treated as an attack the application must defend against.

Known or subsequently discovered vulnerabilities within authentic dependencies are considered a relevant security concern and may require dependency updates or other mitigations.

Data processed by trusted application components are not inherently trusted and will still be treated according to the threat model's input and integrity assumptions.



## DEC-xxx:
**Status:**
**Date:**

### Context

### Decision

### Rationale

### Alternatives Considered

### Consequences