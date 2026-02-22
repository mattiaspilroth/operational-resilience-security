# OT Identity Architecture: Federation, PAM, and Residual Risk

Identity architectures in OT operate under the same constraints that shape all long-lifecycle operational infrastructure: limited change capacity, intermittent connectivity, and operational accountability that prioritizes continuity over administrative convenience.

Modern identity models emphasize federation and centralized authentication. OT environments impose structural limits on how far those models can extend. Identity controls must remain viable over decades, operate under partial isolation, and degrade safely when external systems fail.

This paper examines three common identity patterns, the risks they redistribute, and why no single model resolves the underlying tensions. It compares isolated, trusted, and federated approaches, then addresses federation scope, third-party access, and residual risk.

## Identity as an architectural constraint in OT

OT identity infrastructure operates under constraints that IT rarely encounters:

* Connectivity may be intermittent or deliberately restricted
* Time synchronization cannot be assumed as a universal invariant
* Administrative authority is distributed across organizational boundaries
* Recovery from failure must be possible without external dependencies

These constraints shape which identity patterns can be sustained in practice.

This discussion focuses on human identity. Machine and application identities form a larger and often less controlled surface, but they introduce different technical and lifecycle constraints and are not treated here.

## Common OT identity patterns

### Option A: Fully isolated local identities

In this model, control systems authenticate users locally. Accounts are defined and managed per system or per site, often using local directories or embedded authentication mechanisms.

**Strengths:**

* No dependency on external identity providers
* Predictable failure modes
* High resilience under isolation

**Limitations:**

* Poor scalability across sites or systems
* Inconsistent access governance
* Difficult to audit centrally

**Observed degradation patterns:**

Without sustained investment in local identity management, this model predictably degrades:

* Weak or reused passwords
* Delayed deprovisioning
* Credentials written down or shared
* Orphaned accounts
* Break-glass access becoming routine

This model prioritizes availability and diagnosability but struggles to meet modern governance expectations.

### Option B: Centralized identity via forest trust or shared domain

Here, OT systems rely on a central directory, typically through domain trust or shared forest membership. This is the most common pattern in brownfield environments, often inherited from earlier infrastructure decisions rather than deliberately selected.

**Strengths:**

* Centralized policy enforcement
* Unified lifecycle management
* Improved auditability

**Limitations:**

* Expands trust boundaries deeply into OT
* Couples OT availability to IT directory health
* Introduces systemic blast radius

**Infrastructure-level implications:**

* Kerberos and delegation cross boundaries
* NTLM relay paths propagate
* Group Policy may traverse trusts
* AD-native lateral movement tooling remains effective
* Replication and RPC create standing connectivity

If IT is compromised, pre-existing pathways into OT may be available by design.

### Option C: Federated identity with privileged access management (PAM)

This model separates routine identity from high-consequence authority.

Federation supports visibility, reporting, and low-risk interaction. Privilege is mediated through PAM, jump hosts, or local controls. In some environments, operator control remains entirely non-federated.

**What federation means:**

Authentication is based on cryptographically signed assertions rather than shared directory infrastructure. OT validates the signature, not the provider runtime.

This removes replication dependency but replaces it with requirements for key custody, validation data, and time integrity.

**Strengths:**

* Central lifecycle control
* MFA enforcement
* No Kerberos or replication dependency
* Fast revocation

**Limitations:**

* New dependency on IdP integrity
* Requires durable token and key management
* Dependent on downstream enforcement
* Limited by application compatibility in brownfield environments

This is a balancing model, not a perfect one.

**Practical adoption constraints:**

PAM platforms are complex infrastructure with their own availability, upgrade, and degradation characteristics. They must be managed as carefully as the access they mediate.

In brownfield environments, legacy applications often cannot consume federation tokens or be modified within vendor validation boundaries. The practical adoption ceiling is frequently defined by application capability rather than architectural intent.

## What federation actually solves

Federation addresses real operational and security problems.

It reduces password reuse, weak credentials, and shared identities. It enables rapid revocation, consistent deprovisioning, and centralized MFA. Unlike forest trust, it does not couple OT availability to directory replication or Kerberos infrastructure.

These are significant operational improvements.

In environments where identity sprawl, credential hygiene, and revocation speed represent the dominant risk factors, federation can materially improve both security posture and operational sustainability.

## Scoping federation: where the boundary goes

Federation can assert identity while leaving process authority to additional controls.

It can reasonably support:

* Read-only views
* Historians
* Analytics
* Documentation access
* Personalization

Actions that change plant state require additional layers reflecting accountability, context, and risk. Where consequence is asymmetric, authority remains local.

## Third-party and vendor access: where authority must remain local

External parties perform a large portion of privileged activity in OT: commissioning, maintenance, troubleshooting, upgrades. Connectivity is often delivered by IT, but responsibility for outcome remains with the site.

Federation can identify who is connecting. It cannot determine whether the proposed action is safe in the current plant context.

This is where PAM becomes the authority boundary.

**PAM provides:**

* Local approval
* Context-aware authorization
* Session control
* Ability to terminate unsafe activity
* Emergency mechanisms with accountability

These capabilities require someone present and attentive. Active supervision is common during commissioning and exceptional during routine maintenance. The resulting gap reflects a familiar condition: responsibility and control reside in different places, and no actor governs the whole.

Without local authority, responsibility and control diverge, and unmanaged risk accumulates between them.

## Residual risk and risk redistribution

Each identity pattern redistributes risk rather than eliminating it.

| Risk dimension        | Option A (Local) | Option B (Forest Trust) | Option C (Federation + PAM)         |
| --------------------- | ---------------- | ----------------------- | ----------------------------------- |
| Primary concentration    | Site discipline  | IT directory integrity  | IdP integrity and scope control     |
| Blast radius             | Local            | Cross-boundary systemic | Scoped if enforcement holds         |
| Governance burden        | Entirely site    | Shared, unevenly        | Shared, differently distributed     |
| Architectural weak point | Credential decay | Lateral movement        | Token minting or scope violation    |
| Long-term drift          | Visible, local   | Silent, wide            | Dependent on enforcement durability |

### Identity provider compromise

A compromised IdP can mint tokens at scale. If federation is limited to visibility, exposure differs from infrastructure trust compromise.

### Downstream enforcement fragility

If one system mishandles claims, containment collapses.

## What shifts and what does not

**Option A:** All burden remains local. Maximum autonomy. Maximum governance fragility.

**Option B:** Identity management shifts to central IT. OT retains operational accountability but cedes identity authority. IT compromise expands into OT by design.

**Option C:** Routine identity governance shifts centrally. Privilege and consequence management remain local. New dependencies (IdP availability, time sync, key rotation) are introduced.

Over long operational lifecycles, models drift as exceptions, staffing changes, and local workarounds accumulate. Central mechanisms weaken, exceptions accumulate, and environments migrate toward informal control.

## Residual tensions that cannot be eliminated

No identity architecture eliminates the tension between centralized governance and operational resilience. Each model trades visibility for autonomy, efficiency for blast radius, or manageability for dependency.

The goal is not to find the correct model. It is to choose where residual risk resides, ensure it is visible, and verify that failure modes are survivable by the teams who will live with them.

## Implications for identity design in OT

The identity model chosen for an OT environment is less about feature completeness and more about survivability under stress. The following implications distinguish structural minimums from lifecycle realities.

### Architectural rules

These are design constraints required to preserve process safety and local authority under failure conditions:

* **Keep authority for high-consequence actions under OT governance.** External systems must not dictate local process safety.

* **Do not require federation for operator control or engineering changes to process state.** Core operations must remain possible during IdP or network outages.

* **Design explicit fallback paths for identity system failure.** Do not rely on improvised break-glass procedures when the primary authentication path fails.

* **Prefer architectures that fail visibly rather than silently.** Operators should know immediately when trust mechanisms or dependencies degrade.

### Operational realities

These reflect structural friction in long-lifecycle industrial environments:

* **Plan for degradation over operational lifecycles.** Systems will operate long after vendor support and initial project structures expire.

* **Expect governance erosion and design containment accordingly.** Local workarounds will accumulate; scoped authority and network segmentation become the final containment layers.

* **Treat time synchronization and IdP availability as operational dependencies, not assumptions.** Token validation and PKI mechanisms fail immediately when these underlying services degrade.

* **Understand infrastructure-level implications of directory trust.** Domain membership is not only an identity decision, but an expansion of systemic blast radius.

Identity in OT is not about elegance. It is about sustaining operational authority under stress for decades and knowing where that authority will fail first.
