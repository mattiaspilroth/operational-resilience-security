# Operational Resilience & OT Security

Practitioner analysis of long-lifecycle security in high-consequence industrial environments.

Drawn from architecture work across production sites where long lifecycles, limited change capacity, regulatory obligations, and operational accountability shape what can realistically be sustained.

The central question:

**Which security controls remain durable under operational reality, and which degrade predictably despite appearing sound on paper?**

These papers examine structural constraints, recurring failure patterns, and the architectural properties required for resilience when consequences are physical, not only informational.

## The papers

Each paper addresses a distinct pattern and can be read independently. Together they describe how security posture evolves under sustained operational pressure.

### Structural Constraints

**[Why OT Infrastructure Appears Static](./papers/01_structural_constraints/why_ot_infrastructure_appears_static.md)**  
Stability in continuous process industries is often an engineered response to asymmetric risk rather than technical stagnation. Examines validated configurations, lifecycle economics, vendor authority boundaries, and why ignoring these constraints leads to security strategies that cannot be sustained.

**[Silent Degradation Under IT/OT Convergence](./papers/01_structural_constraints/silent_degradation_under_it_ot_convergence.md)**  
Redundant IT infrastructure inside segmented OT zones can degrade invisibly when health signals do not reach actors with authority to intervene. The gap is often not the absence of signals, but the absence of a clearly defined owner for acting on them.

### Identity and Trust

**[OT Identity Architecture: Federation, PAM, and Residual Risk](./papers/02_identity_and_trust/ot_identity_architecture_federation_pam_residual_risk.md)**  
A structural analysis of common identity models in OT. Explores how federation, isolation, and hybrid approaches redistribute rather than eliminate risk, and why authority for high-consequence actions must remain clearly defined.

**Part 1: [Trust Decay in Constrained OT Environments](./papers/02_identity_and_trust/trust_decay_in_constrained_ot_environments.md)**  
Certificate validation assumes trust material is continuously obtainable. In segmented OT architectures, that assumption may not hold. Trust erosion can remain latent until operational stress reveals it.

**Part 2: [Trust Flow in Constrained OT Environments](./papers/02_identity_and_trust/trust_flow_in_constrained_ot_environments.md)**  
Defines the properties required for validation to occur predictably and repeatedly inside constrained zones. Written as architectural requirements to prevent the failure modes identified in Part 1.

### Strategy and Governance

**[Compliance and Consequence: Competing Priorities in OT Security](./papers/03_compliance_and_consequence/compliance_and_consequence_competing_priorities.md)**  
Examines why compliance-driven programs and resilience-driven programs diverge over time. Analyzes the structural incentives behind that divergence and outlines what operationalizing consequence-oriented security requires.

## Perspective

These papers favor:

* Architectural reasoning beyond checklist interpretation
* Observed operational behavior over design intent
* Long-term durability over short-term elegance
* Contextual allocation of controls rather than universal prescriptions

No control category is universally correct. Architectural fit determines durability.

The goal is practical clarity, not comprehensive coverage.

## Discussion

Practitioners who have observed similar or contradictory patterns are welcome to engage.

Disagreement grounded in operational experience is particularly valuable.


## About

Written by **Mattias Pilroth**, working with enterprise OT security architecture across European chemical and process industry environments.

Independent analytical work. Does not represent the positions of any employer or client. All examples are abstracted from general operational patterns. No proprietary, confidential, or organizationally identifying information is included.

[LinkedIn](https://www.linkedin.com/in/mattiaspilroth)