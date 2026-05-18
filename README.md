# Mattias Pilroth — Analytical Archive

Current work is published at [mattiaspilroth.com](https://mattiaspilroth.com).

This repository is an archived collection of analytical papers. The papers examine structural constraints, recurring failure patterns, and the architectural properties required for resilience in high-consequence industrial environments. They represent the analytical foundation that the current framework builds on, not the framework itself.

The central question running through this archive: which security controls remain durable under operational reality, and which degrade predictably despite appearing sound on paper?

## Archive contents

### Operational reality

**[Why OT Infrastructure Appears Static](./papers/01_structural_constraints/why_ot_infrastructure_appears_static.md)**  
Stability in continuous process industries is often an engineered response to asymmetric risk rather than technical stagnation. Examines validated configurations, lifecycle economics, vendor authority boundaries, and why ignoring these constraints leads to security strategies that cannot be sustained.

**[Silent Degradation Under IT/OT Convergence](./papers/01_structural_constraints/silent_degradation_under_it_ot_convergence.md)** 
Redundant IT infrastructure inside segmented OT zones can degrade invisibly when health signals do not reach actors with authority to intervene. The gap is often not the absence of signals, but the absence of a clearly defined owner for acting on them.

**[Compliance and Consequence: Competing Priorities in OT Security](./papers/03_compliance_and_consequence/compliance_and_consequence_competing_priorities.md)**  
Examines why compliance-driven programs and resilience-driven programs diverge over time. Analyzes the structural incentives behind that divergence and outlines what operationalizing consequence-oriented security requires.

### Identity and trust in OT

**[OT Identity Architecture: Federation, PAM, and Residual Risk](./papers/02_identity_and_trust/ot_identity_architecture_federation_pam_residual_risk.md)**  
A structural analysis of common identity models in OT. Explores how federation, isolation, and hybrid approaches redistribute rather than eliminate risk, and why authority for high-consequence actions must remain clearly defined.

**Part 1: [Trust Decay in Constrained OT Environments](./papers/02_identity_and_trust/trust_decay_in_constrained_ot_environments.md)**  
Certificate validation assumes trust material is continuously obtainable. In segmented OT architectures, that assumption may not hold. Trust erosion can remain latent until operational stress reveals it.

**Part 2: [Trust Flow in Constrained OT Environments](./papers/02_identity_and_trust/trust_flow_in_constrained_ot_environments.md)**  
Defines the properties required for validation to occur predictably and repeatedly inside constrained zones. Written as architectural requirements to prevent the failure modes identified in Part 1.

## Current framework

The SOR Framework and its companion papers are available at [mattiaspilroth.com](https://mattiaspilroth.com). The framework operationalises the consequence-derived investment model that the papers in this archive point toward but do not deliver.

Recommended reading order for new visitors: start at mattiaspilroth.com.

## About

Written by Mattias Pilroth, OT security architect working on consequence-derived investment frameworks for process industry environments. Operator background: six years of end-to-end operational responsibility at a SEVESO-classified chlorovinyl production facility. Current work spans enterprise OT security architecture across 14 chemical manufacturing sites in 8 European countries.

Independent analytical work. Does not represent the positions of any employer or client. All examples are abstracted from general operational patterns. No proprietary, confidential, or organisationally identifying information is included.

[mattiaspilroth.com](https://mattiaspilroth.com) · [LinkedIn](https://www.linkedin.com/in/mattiaspilroth)
