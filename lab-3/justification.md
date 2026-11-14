# Lab 3: Architecture Justification

**System:** Patient Health Record Consent Management System (Problem Statement #13)

**Name:** Mohammed Tahir Siddique | **SRN:** PES2UG24AM092

## Architecture Selection

We chose **Layered Architecture** for the Patient Health Record Consent Management System.

## Architectural Choice

The system is organised into three layers. The Presentation Layer holds the Patient Portal and the Clinic Portal. The Business Layer holds the Consent Manager, Record Access Service, Notification Service and Audit Logger. The Data Layer holds the Consent Repository, Health Record Repository and Audit Trail Store. Each layer uses only the interfaces of the layer directly below it.

## Two Reasons

**Reason 1: Consent is enforced in one place.** Every request for a health record must pass a consent check (FR-004). In the layered design, both portals can reach records only through the Record Access Service in the Business Layer, and that service always calls the Consent Manager first. The rule is written once and no screen can skip it. With microservices, the same check would have to be repeated or coordinated across several services.

**Reason 2: The system is small and its data must stay consistent.** There are only two user groups and a small set of functions. A consent, its expiry time and its audit entry must be saved together, and a revocation must take effect immediately (FR-002). One layered application with a single database transaction handles this simply. Microservices would add distributed transactions and deployment effort that this system does not need.

## Security Advantage

The Data Layer is never exposed to the portals. Health records, consents and the audit trail can be reached only through Business Layer interfaces, so an attacker who compromises a portal still cannot query the stored data directly. In addition, the Audit Logger is the only component that writes to the append-only Audit Trail Store, so every grant, revoke and access event is recorded in one controlled place (NFR-001).

## Performance Benefit

All layers run in a single deployment, so the consent check is an in-process call and not a network call between services. A record access needs one consent lookup and one record query, with no service-to-service hops. This keeps the response time low and predictable, and helps meet the target of consent validation within 500 ms for 95% of requests (NFR-002).
