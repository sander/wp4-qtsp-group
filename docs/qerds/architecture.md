# Architecture overview for QERDS in WE BUILD

## Context

### Purpose of this document

This document specifies the high-level architecture for the [provision of qualified electronic registered delivery services (QERDS)](README.md) within WE BUILD.
It aims to guide the specification, development, testing and implementation of QERDS.
It complements the [WE BUILD architecture documentation](https://github.com/webuild-consortium/wp4-architecture) which specifies, among other topics, the transmission of data within WE BUILD in general.

### Definitions

In WE BUILD, QTSPs as defined under [eIDAS] Art. 3(20) provide pre-production ERDS as defined under Art. 3(16)(g) and (h), technically ready to be audited for qualification as defined under Art. 3(17), for QERDS as defined under Art. 3(37).

[eIDAS]: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A02014R0910-20241018

## Technical specifications for QERDS

### Functional decomposition

The following decomposition is inspired by [ETSI EN 319 521 v1.1.1], [ETSI EN 319 522-1 v1.2.1](https://www.etsi.org/deliver/etsi_en/319500_319599/31952201/01.02.01_60/en_31952201v010201p.pdf), and [ETSI TS 119 471 v1.1.1](https://www.etsi.org/deliver/etsi_ts/119400_119499/119471/01.01.01_60/ts_119471v010101p.pdf).

[ETSI EN 319 521 v1.1.1]: https://www.etsi.org/deliver/etsi_en/319500_319599/319521/01.01.01_60/en_319521v010101p.pdf

- **QERDS service:** An electronic service which supports the following QERDS processes. It is provided by a QTSP which is on the *trusted list* upon auditing for conformance to general requirements and to specific EBW interoperability requirements and upon qualification for QEAA issuance.
    - **Message submission:** The *sender* uses the *QTSP* to submit a document or notification to a *wallet*.
    - **Message retrieval:** The *recipient* uses the *QTSP* to retrieve a document or notification in their *wallet*.
    - **Evidence retrieval:** The *QTSP* provides timestamped, sealed evidence to the *wallet* of the *sender* or *recipient* about the transmission.
    - **Message relay:** The *QTSP* relays messages from another ERDS, potentially a gateway during the European Business Wallet derogation period.
    - **Common service access:** The *QTSP* accesses message routing, trust management, capability management, and governance functions from common services such as the *European Digital Directory*.
- **Identity proofing service:** an electronic service by which the identity and additional attributes of an applying *subscriber* are verified. The verification process uses evidence attesting to the required identity attributes, including evidence from *PID/EAA presentation*.
- **Qualified electronic sealing service:** an electronic service by which the *QTSP* attaches or logically associates with data an qualified electronic seal to ensure the data’s origin and integrity.
- **Qualified time stamping service:** an electronic service by which the *QTSP* binds data to a particular time establishing evidence that the latter data existed at that time.

### Policy and security requirements

#### QERDS service

The requirements from [(EU) 2025/1944](https://data.europa.eu/eli/reg_impl/2025/1944/oj) Annex apply, based on [ETSI EN 319 521 v1.1.1].

#### Identity proofing service

The requirements from [eIDAS] Art. 24(1a) and [ETSI TS 119 461 v2.1.1](https://www.etsi.org/deliver/etsi_ts/119400_119499/119461/02.01.01_60/ts_119461v020101p.pdf) apply.

#### Qualified electronic sealing service

Where required by the applicable QERDS policy/profile, the QTSP applies a qualified electronic seal to service-generated data or evidence so that origin and integrity can be demonstrated.

This architecture document does not redefine the policy or conformity requirements for qualified sealing. Those are inherited from the applicable legal and standards framework and from the QTSP's qualified sealing service documentation and controls.

#### Qualified time stamping service

The QERDS architecture relies on trusted time information for evidence creation, event ordering, and traceability, where proof of time is required.

This architecture document does not redefine the policy or conformity requirements for qualified time stamping. Those are inherited from the applicable legal and standards framework and from the QTSP's time-stamping service documentation and controls.

### Deployment model and interfaces

The visualisation below represents a value chain, in which the primary data flows from left to right. The technical control flow may be reverse, for example using service request-response patterns.

TBD

### Data flows and interactions

#### Protocol profiles

TBD

### Example use case scenarios

TBD

## Deviations from European Business Wallets

WE BUILD operates as a pre-production pilot environment and is not identical to the final legally mandated ecosystem.

Accordingly, some European Business Wallet roles, trust components, and operational arrangements may be simulated, stubbed, or implemented with transitional pilot-specific configurations for interoperability testing.

Examples may include:
- pilot registries (including fictitious or simulated registry data);
- pilot trust-status sources, including WE BUILD trusted-list style mechanisms;
- gateway components used during migration or derogation periods;
- non-production governance workflows and consortium-specific conventions.

Any such deviation should be explicitly documented in the relevant WE BUILD artefact (e.g. ADR, WBCS, or profile documentation), including:
- scope of the deviation;
- reason for the deviation;
- expected duration (if known);
- impact on interoperability testing;
- migration conditions toward the target-state arrangement.

### Out of scope

This document does not define:
- Member State-specific policy choices, approval criteria, or national extensions;
- long-term production operating models or operational SLAs;
- legal qualification decisions or conformity assessment procedures;
- provider-specific internal control implementations;
- detailed wire-level protocol bindings (unless explicitly stated elsewhere).

These topics may be addressed in ADRs, WBCS, provider documentation, or other WE BUILD/WP4 artefacts as applicable.
