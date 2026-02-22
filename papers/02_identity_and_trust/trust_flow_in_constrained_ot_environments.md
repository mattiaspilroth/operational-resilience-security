# Trust Flow in Constrained OT Environments

## Why trust requires design

In isolated and segmented operational environments, certificate validation cannot rely on spontaneous reachability.

When trust mechanisms depend on services the architecture cannot guarantee, execution will become inconsistent.
Under pressure, informal adjustments replace design.

For trust to remain reliable, the movement, availability, and lifecycle of trust material must be engineered deliberately.

This document defines the properties required for that to occur.
It does not prescribe a specific implementation.

## What must remain true

A trust architecture inside a constrained zone must allow validation to occur **predictably, repeatedly, and without improvisation**.

If this cannot be guaranteed, drift toward exception handling should be expected.

## Required properties of survivable trust

### Explicit ownership of trust state

Someone must be responsible for ensuring that trust material remains current, correct, and complete.

Without ownership, decay progresses quietly when no one is accountable for detecting it.

### Curated and lifecycle-managed root authorities

Trust anchors cannot remain static for the lifetime of the installation, nor can they be inherited wholesale from general-purpose root programs.

Public root stores are optimized for broad compatibility.
They include authorities unrelated to industrial operation and carry relationships that rarely align with organizational threat models or regulatory expectations.

Updates to public root stores can silently extend or withdraw trust relationships without operator awareness, potentially changing validation outcomes or breaking previously functioning systems.

In high-consequence environments, trust scope must be deliberately constrained. The method of achieving that constraint may vary.

If root sets are not intentionally maintained, new artifacts will fail unpredictably. Under time pressure, emergency imports follow, establishing a pattern that rarely gets documented or reversed.

### Controlled and auditable distribution

Trust material must arrive through defined, repeatable, and observable processes.

If administrators transfer certificates ad hoc, governance loses visibility and assurance becomes personal rather than institutional.

### Deterministic availability of trust material

All elements required for validation, including chains, revocation information, and supporting metadata, must be obtainable within the zone at the moment they are required.

Operation becomes fragile when it depends on optional connectivity or best-effort reachability.

If availability is uncertain, bypass pressure increases and may become routine.

This does not imply that always-online OCSP is required; it implies that whatever revocation approach is chosen (including deliberate non-use with compensating controls) must be explicit, supportable, and locally survivable.

### Deterministic availability of time

Validation depends on a consistent notion of time (e.g., certificate validity periods and freshness of revocation data).

The zone must provide a time source that remains reliable under isolation, or define explicitly how validation behaves if time cannot be trusted.

### Local completeness of validation paths

Every system performing validation must be able to obtain the full set of inputs necessary to reach a decision from within the zone.

Partial information produces timeouts, workarounds, or relaxed enforcement.

### Independence from external services

Validation must succeed even if no connection to enterprise or internet resources exists.

Any requirement for external resolution introduces dependency that may conflict with the architecture’s isolation goals.

### Predictable behavior during degraded conditions

The architecture must define how validation behaves when expected inputs are missing.

Examples include failing closed, failing open with compensating controls, or relying on time-bounded cached decisions. What matters is that behavior is defined rather than improvised.

If behavior is undefined, local interpretation tends to replace policy.

### Ability to demonstrate runtime execution

It must be possible to verify that validation is not only configured but actively occurring during operation.

Presence of structure is not evidence of execution.

These properties are not independent. In practice, they create tensions that must be resolved through design choices.

Deterministic availability often favors pre-staging all trust material. Lifecycle management requires periodic updates. Independence from external services limits distribution mechanisms. Predictable degraded behavior may sacrifice availability for security, or vice versa.

The goal is not to maximize each property independently. It is to achieve sufficient capability in each while understanding which tensions the architecture resolves in favor of availability, which in favor of assurance, and why.

## What happens if these properties are absent

When environments lack these characteristics, familiar patterns emerge.

Roots are imported manually.
Revocation checking is disabled or bypassed.
Distribution points are ignored.
Default trust programs are inherited without examination.
Self-signed certificates proliferate as substitutes for managed trust.
Exceptions accumulate without record.

Systems continue to function, but assurance becomes difficult to demonstrate at runtime. In practice, tolerance has replaced assurance.

## What these properties enable

When these properties are engineered deliberately, trust becomes operational rather than aspirational.

Installations proceed without improvisation.
Recovery becomes repeatable.
Change is predictable.
Audits can verify behavior rather than diagrams.

Continuity and assurance stop competing with one another.

Trust becomes a dependency that can be operated, not tolerated.

## Implementation latitude

This document does not mandate technology, topology, or product.

Multiple implementations may satisfy these properties.

Any proposal that cannot is unlikely to remain reliable under the constraints typical of production OT.