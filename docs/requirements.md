# Requirements

## Authentication

### AUTH-001: Master password creation

#### Description:
The system shall allow a user create an initial master password used to protect the credential vault.

Acceptance Criteria:
- User can provide a master password.
- Password is checked against strength requirements.
- The system can verify future authentication attempts without storage of the original master password.
- The original master password is never stored.

Priority: Must Have


### AUTH-002: User authentication for vault access

#### Description
The system shall not allow vault access unless the user has successfully authenticated.

#### Acceptance Criteria:
- Vault is inaccessible until successful authentication.
- Vault is accessible once authentication has been successful.
- Unsuccessful authentication atempts must not grant vault access.

Priority: Must Have
21

### AUTH-003: Vault re-secured after a period of inactivity

#### Description
The system shall automatically lock the vault after a period of inactivity.

#### Acceptance Criteria:
- The vault automatically locks after the configured inactivity period.
- Whilst locked, the vaults contents cannot be accessed without successful re-authentication.
- The default period of inactivity is defined by the application.

Priority: Must Have

### AUTH-004: User defined inactivity period
1
#### Description
The system shall allow the user to define the period of inactivity before the vault automatically locks itself

#### Acceptance Criteria:
- The user can configure the inactivity period before the vault automatically locks.
- After the user defined inactivity period, the vault will automatically lock.
- After re-locking, the vault's contents cannot be accessed without successfully re-authenticating to the system.

Priority: Nice to Have


### AUTH-005: Initial authentication setup

#### Description
The system shall guide the user through creating the initial authentication configuration when no valid vault exists.

#### Acceptance Criteria:
- The system detects when there is no valid vault.
- The user is guided through the initial setup.
- A new protected vault is created after successful completion of the initial setup.

Priority: Must Have


## Vault Management

### VAULT-001: Vault data secure at rest

#### Description
Any data stored by the vault must remain secure whilst not in use.

#### Acceptance Criteria:
- The system shall protect stored vault data against unauthorised access if the vault storage is obtained by an attacker.

Priority: Must Have


### VAULT-002: Vault export

#### Description
 The system shall allow the user to export the vault to a portable file that can be imported by another instance of the application.

#### Acceptance Criteria:
 - User can export the current vault.
 - The exported vault can be imported by another instance of the application.
 - The exported vault remains protected against unauthorised access
 
Priority: Should Have


### VAULT-003: Vault import

#### Description
The system shall allow the user to import a vault previously exported by the application.

#### Acceptance Criteria:
- Successfully imported vaults can be accessed following successful authentication.
- The system shall reject vault files that are not recognised as valid exports.
- The system shall verify the integrity and validity of imported vault files before importing them.

Priority: Should Have

### VAULT-004: Vault integrity validation

#### Description
The system shall detect when a vault cannot be verified as valid.

#### Acceptance Criteria
- The system validates a vault's integrity before attempting to use it.
- An invalid vault will not load corrupted or partial credential data.
- The system shall inform the user of an invalid vault that requires recovery, restoration, or replacement.

Priority: Must Have