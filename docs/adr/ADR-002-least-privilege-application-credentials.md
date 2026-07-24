# ADR-002: Principle of Least Privilege for Application Credentials

## Status

Accepted

## Date

2026-07-21

## Context

The Music Server application will require access to a PostgreSQL database to store and retrieve application data.

Using a PostgreSQL administrative or superuser account for the application would create unnecessary security risk. If the application or its credentials were compromised, an attacker could potentially gain administrative control over the database server and perform actions beyond what the application requires.

The system should follow the principle of least privilege by ensuring that application services receive only the permissions necessary to perform their intended functions.

## Decision

The Music Server application will use a dedicated PostgreSQL database account with restricted permissions.

The application account will not use the PostgreSQL superuser or administrative account for routine application operations.

Administrative database credentials will be kept separate from application credentials and will only be used when administrative tasks are required.

Sensitive credentials will not be committed to the Git repository or stored directly in publicly accessible configuration files.

## Rationale

The principle of least privilege reduces the potential impact of a compromised application or exposed credential.

By separating application and administrative credentials:

- A compromised application account has a more limited scope of access.
- An attacker is less likely to gain full administrative control of PostgreSQL.
- Administrative operations require separate credentials.
- Access can be reviewed and revoked independently.
- The architecture follows a common security best practice.

## Security Considerations

The application database account should only have the permissions required by the application.

Database credentials should be stored using an appropriate secret-management mechanism for the deployment environment.

For local development, environment variables or a local `.env` file may be used, provided that sensitive files are excluded from version control.

For future production deployments, a dedicated secret-management solution should be considered.

## Consequences

### Advantages

- Reduces the potential impact of credential compromise.
- Limits the application's database permissions.
- Separates application and administrative responsibilities.
- Supports defense in depth.
- Encourages secure credential management practices.

### Disadvantages

- Requires additional database configuration.
- Administrative tasks require separate credentials.
- Secret management adds operational complexity.

## Future Considerations

Future versions of the project may implement:

- Docker Secrets or an external secrets manager.
- Automated credential rotation.
- More granular database roles.
- Auditing of database access.
- Separate development and production credentials.