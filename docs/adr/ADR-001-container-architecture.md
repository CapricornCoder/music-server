# ADR-001: Container Architecture

## Status

Accepted

## Date

2026-07-21

## Context

The Music Server project requires multiple services that perform different responsibilities, including:

- Music streaming
- Database management
- Reverse proxy and HTTPS
- Future monitoring and backup services

The architecture should be secure, modular, easy to maintain, and representative of production DevSecOps environments.

## Decision

Each major component will run as an independent Docker container connected through a private Docker network.

Only the reverse proxy will expose ports to the host machine.

## Rationale

Separating services into individual containers follows the principle of separation of concerns.

This design provides several advantages:

- Services can be upgraded independently.
- Failures are isolated.
- Internal services remain inaccessible from the public network.
- The architecture closely resembles production deployments.
- Individual services can be secured according to the principle of least privilege.

## Consequences

### Advantages

- Improved security
- Easier maintenance
- Better scalability
- Simplified troubleshooting
- Clear separation of responsibilities

### Disadvantages

- Additional networking complexity
- More configuration files
- Requires understanding Docker networking

## Future Considerations

Future versions of the project may include:

- Monitoring with Grafana and Prometheus
- Centralized logging
- Automated backups
- CI/CD deployment pipeline