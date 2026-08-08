# Requirements

## Authentication

### AUTH-001: Master password creation
#### Description
The system shall allow a user to create an initial master password used to protect the credential vault.

#### Acceptance Criteria:
- User can provide a master password.
- Password is checked against strength requirements.
- The system can verify future authentication attempts without storage of the original master password.
- The original master password is never stored.

**Priority:** Must Have


### AUTH-002: User authentication for vault access
#### Description
The system shall not allow vault access unless the user has successfully authenticated.

#### Acceptance Criteria:
- Vault is inaccessible until successful authentication.
- Vault is accessible once authentication has been successful.
- Unsuccessful authentication attempts must not grant vault access.

**Priority:** Must Have


### AUTH-003: Vault re-secured after a period of inactivity
#### Description
The system shall automatically lock the vault after a period of inactivity.

#### Acceptance Criteria:
- The vault automatically locks after the configured inactivity period.
- Whilst locked, the vault's contents cannot be accessed without successful re-authentication.
- The default period of inactivity is defined by the application.

**Priority:** Must Have

### AUTH-004: User-defined inactivity period
#### Description
The system shall allow the user to define the period of inactivity before the vault automatically locks itself.

#### Acceptance Criteria:
- The user can configure the inactivity period before the vault automatically locks.
- After the user-defined inactivity period, the vault will automatically lock.
- After re-locking, the vault's contents cannot be accessed without successfully re-authenticating to the system.

**Priority:** Nice to Have


### AUTH-005: Initial authentication setup
#### Description
The system shall guide the user through creating the initial authentication configuration when no valid vault exists.

#### Acceptance Criteria:
- The system detects when there is no valid vault.
- The user is guided through the initial setup.
- A new protected vault is created after successful completion of the initial setup.

**Priority:** Must Have


## Vault Management

### VAULT-001: Vault creation
#### Description
The system shall allow the user to create a new vault.

#### Acceptance Criteria:
- When no vault has previously been configured, the system shall allow the user to either create a new vault or import a vault.
- When the user chooses to create a new vault, the system shall guide the user through the required initial authentication setup.
- A new protected vault shall only be created after the initial authentication setup has been successfully completed.

**Priority:** Must Have


### VAULT-002: Vault export
#### Description
 The system shall allow the user to export the vault to a portable file that can be imported by another instance of the application.

#### Acceptance Criteria:
 - User can export the current vault.
 - The exported vault can be imported by another instance of the application.
 - The exported vault remains protected against unauthorised access.
 
**Priority:** Should Have


### VAULT-003: Vault import
#### Description
The system shall allow the user to import a vault previously exported by the application.

#### Acceptance Criteria:
- Successfully imported vaults can be accessed following successful authentication.
- The system shall reject vault files that are not recognised as valid exports.
- The system shall verify the integrity and validity of imported vault files before importing them.

**Priority:** Should Have


### VAULT-004: Vault integrity validation
#### Description
The system shall detect when a vault cannot be verified as valid.

#### Acceptance Criteria
- The system validates a vault's integrity before attempting to use it.
- An invalid vault will not load corrupted or partial credential data.
- The system shall inform the user of an invalid vault that requires recovery, restoration, or replacement.

**Priority:** Must Have


## Credential Management

### CRED-001: Credential creation
#### Description
The system shall allow the user to create credentials that contain an identifier for the account or service it belongs to, a username, and a password.

#### Acceptance Criteria
- The user can enter into the system a username:password which is then stored in the vault.
- The user cannot create more than one credential with the same account/service and username combination.

**Priority:** Must Have


### CRED-002: Credential retrieval
#### Description
The system shall allow the user to select a stored username:password pair for use.

#### Acceptance Criteria
- The system shall make the original stored credential available to the authenticated user.

**Priority:** Must Have


### CRED-003: Credential editing
#### Description
The system shall allow the user to change the information of a username:password pair that is already stored in the vault

#### Acceptance Criteria
- The user can select an already existing username:password pair, then change either or both of these details with the new changes stored in the vault and the old details discarded.
- The user cannot change a credential pair to be the same as an already existing credential pair. If this happens, the user is notified and the original data is maintained with no changes.

**Priority:** Must Have


### CRED-004: Credential deletion
#### Description
The system shall allow the user to delete an already stored username:password pair.

#### Acceptance Criteria
- The system shall allow the user to select a credential to be deleted.
- Deleted credentials must not subsequently become accessible through the application.

**Priority:** Must Have


### CRED-005: Credential searching
#### Description
The system shall allow users to search stored credentials.

#### Acceptance Criteria
- The system displays all credential pairs containing the supplied username to the user.
- The system does not display any credential pairs that do not contain the supplied username.
- The system will notify the user if there are no credentials stored in the vault with the supplied username.

**Priority:** Should Have


## Password Assistance

### PASS-001: Secure password suggestion
#### Description
The system shall suggest to the user a password that meets a predefined security standard.

#### Acceptance Criteria
- A password that meets the pre-defined security standard is generated when requested by the user.
- The system shall not suggest a password that is already in use by a credential already stored in the vault
- The suggested password shall not violate any of the predefined security standard rules.

**Priority:** Must Have


### PASS-002: Password suitability evaluation
#### Description
The system shall evaluate user-defined passwords for their suitability as passwords.

#### Acceptance Criteria
- A user-defined password is evaluated against predefined security standard rules. 
- The user is notified if a supplied password meets the system's standard rules or not.
- A user supplied password is stored even if it does not meet the pre-defined security standard rules.

**Priority:** Must Have

### PASS-003: User-defined password security standard rules
#### Description
The system shall allow the user to define the security standard rules by which new passwords should be evaluated and generated.

#### Acceptance Criteria
- User-defined security standard rules shall be saved and persist between application sessions.
- Password generation shall use the currently configured security rules.
- Password evaluation shall use the currently confugured security rules.
- If user-defined security standard rules cannot be found, the system shall default to the pre-defined ruleset.

**Priority:** Nice to Have


## Notes Management

### NOTE-001: Create secure notes
#### Description
The system shall allow users to create text notes that will be stored in the vault.

#### Acceptance Criteria
- User created text notes will be stored in the vault.
- The system shall protect stored notes data against unauthorised access if the vault storage is obtained by an attacker.

**Priority:** Must Have

### NOTE-002: Retrieve stored secure notes
#### Description
The system shall allow users to select and view the contents of a secure note.

#### Acceptance Criteria
- A selected secure note shall be recovered and displayed to the user.

**Priority:** Must Have


### NOTE-003: Edit existing secure notes
#### Description
The system shall allow users to update and change the contents of a secure note.

#### Acceptance Criteria
- Changes made to a secure note shall be saved in the vault.
- The previous versions of the secure note shall no longer be accessible.
- The user shall be notified if the update to the secure note was successful or not.

**Priority:** Must Have

### NOTE-004: Deletion of existing secure notes
#### Description
The system shall allow users to delete existing secure notes.

#### Acceptance Criteria
- The system shall allow the user to select a secure note to be deleted.
- Deleted secure notes must not be accessible through the application.

**Priority:** Must Have

## Audit

### AUD-001: Record auditable vault data actions
#### Description
The system shall maintain an audit trail of significant actions performed against vault data.

#### Acceptance Criteria
- The system shall record whenever a credential is created, edited, or deleted.
- The system shall record whenever a secure note is created, edited, or deleted.
- Each audit entry shall record the time and date in which the action occured.
- Each audit entry shall identify type of action performed.
- Each audit entry shall identify the type of data entity affected.
- Each audit entry shall identify the vault associated with the affected data.
- Each audit entry shall record whether the attempted action was completed successfully or failed.

**Priority** Should Have

### AUD-002: Record auditable system events
#### Description
The system shall maintain an audit trail of significant application events affecting the vault or its security state.

#### Acceptance Criteria
- The system shall record significant authentication events.
- The system shall record significant vault state changes, including locking and unlocking.
- The system shall record vault import and export events.
- The system shall record vault integrity failures.
- Each audit entry shall record the date and time at which the event occurred.
- Each audit entry shall record the tpye of event that occurred.
- Each audit entry shall record the outcome of the event when outcomes are applicable.

**Priority:** Should Have


## Security (Non-Functional)

### SEC-001: Protection of sensitive data at rest
#### Description
The system shall protect sensitive vault data against disclosure while the data is at rest.

#### Acceptance Criteria:
- An attacker obtaining a copy of the vault shall not gain access to protected credential or secure-note contents solely by possessing a copy of that vault.
- Sensitive vault contents shall remain protected while the applciation is closed.
- Access to protected vault contents shall require successful authentication.
- Exported vault data shall provide the same level of protection against unauthorised disclosure.

**Priority:** Must Have


### SEC-002: Protection of audit information
#### Description
The system shall prevent audit record from exposing sensitive vault or authentication data.

#### Acceptance Criteria:
- Audit records shall not contain plaintext passwords.
- Audit records shall not contain secure-note contents.
- Audit records shall not contain the master password or other authentication secrets.
- Audit records shall be protected against unauthorised access.

**Priority:** Must Have


### SEC-003: Protection of sensitive data in application logging
#### Description
The system shall prevent diagnostic and application logging from exposing any sensitive vault or authentication data.

#### Acceptance Criteria
- Application logs shall not contain plaintext passwords
- Application logs shall not contian secure-note contents.
- Application logs shall not contain the master password or other authentication secrets.
- Error and exception handling and reporting shall not expose sensitive vault contents.

**Priority:** Must Have


### SEC-004: Protection of user's authentication secrets
#### Description
The system shall minimise exposure of the user's authentication secrets during the authentication process, and shall not persist those secrets in their original form.

#### Acceptance Criteria
- Authentication secrets entered by the user shall be masked by default during entry.
- The original authentication secret shall not be written to persistent storage.
- Authentication secrets shall not remain accessible to the application longer than required for authentication.

**Priority:** Must Have


## Maintainability

### MAIN-001: Modular extensible codebase
#### Description
The code base shall be structured so that individual areas of functionality can be modified or extended with minimal impact on the rest of the application.

#### Acceptance Criteria
- Application components shall have clearly defined responsibilities.
- Changes to one area of functionality shall not require changes to other unrelated application components.
- New functionality shall be capable of introduction through extension or addition to relevant components, without requiring modification to unrelated application components.
- Dependencies between components shall be explicit and limited to those required for their responsibilities.

**Priority:** Must Have

### MAIN-002: Automated unit testing
#### Description
The codebase shall be supported by automated unit tests that validate expected behaviour adn help detect regressions through the development process.

#### Acceptance Criteria
- New or modified testable functionality shall be accompanied by appropriate unit tests.
- Unit test shall validate both expected behaviour and relevant failure conditions where applicable.
- Existing automated tests shall continue to pass unless intentional requirement changes alter the expected behaviour.
- When expected behaviour changed intentionally, the affected tests shall be updated to reflect the changed requirements.
- The project's unit test suite shall be executable as a single automated test run.

**Priority:** Must Have


## Performance


## Extensibility