# Generic Master Prompt -- DFD Threat Model (Technology Agnostic)

## Purpose

Use this prompt to perform a structured threat model of any system using
a Data Flow Diagram (DFD), focusing on trust boundaries and boundary
traversals.

## Master Prompt

-   Perform a Data Flow Diagram (DFD) Threat Model Security Analysis
    with emphasis on Trust Boundaries.
-   Use STRIDE (Spoofing, Tampering, Repudiation, Information
    Disclosure, Denial of Service, Elevation of Privilege).
-   Use DREAD (Damage, Reproducibility, Exploitability, Affected Users,
    Discoverability) for qualitative risk scoring.
-   Assume sensitive data is processed (replace with your domain: PHI,
    PII, PCI, Trade Secrets, etc.).

## DFD Tech Stack (Replace With Your Stack)

-   **Cloud Provider:** `<Insert Cloud / On-Prem / Hybrid>`{=html}
-   **Hosting Model:**
    `<Containers / VMs / Serverless / PaaS / Bare Metal>`{=html}
-   **Application Runtime:** `<Language / Framework>`{=html}
-   **Identity Provider:** `<IdP / IAM Platform>`{=html}
-   **Datastores:** \<DB Type(s)\>
-   **Messaging / Integration:**
    `<Queues / APIs / Event Streams>`{=html}
-   **External Dependencies:**
    `<Third Parties / SaaS / Partners>`{=html}

Comment: Clearly list technologies. Each platform boundary (cloud,
managed service, SaaS, database, etc.) should be evaluated as a
potential trust boundary traversal.

## Required Analysis

1.  Analyze the DFD with emphasis on data traversals across trust
    boundaries.
2.  Identify all trust boundaries and describe each data flow crossing
    them.
3.  For each trust boundary crossing:
    -   Identify STRIDE threats.
    -   Provide DREAD-based qualitative risk.
    -   Recommend at least two strong security controls.
    -   Validate existing controls against the strong control
        definition.
    -   Explicitly recommend missing strong controls.
4.  If the DFD lacks clarity (undefined actors, unclear flows, missing
    boundaries), ask targeted clarifying questions before proceeding.
5.  If the DFD states TLS is used, treat TLS as baseline only (not a
    strong control).

Only provide detailed analysis for trust boundary traversals.

## Definition -- Strong Security Controls (Technology Neutral)

The following are considered strong controls and must be explicitly
recommended where appropriate:

-   Mutual TLS (mTLS) for service-to-service authentication
-   Network segmentation (security groups, firewall rules,
    microsegmentation)
-   IAM with least privilege and just-in-time access
-   Multi-Factor Authentication (MFA) for privileged or sensitive access
-   Private connectivity (Private Endpoints, Private Links, VPC Peering,
    etc.)
-   IP allow lists restricting trusted sources
-   Strong session management (device binding, IP fingerprinting, token
    binding)
-   Centralized authentication with strong conditional access policies
-   OAuth2/OIDC with scoped access tokens
-   Logging, monitoring, and anomaly detection focused on boundary
    crossings
-   Intrusion Prevention Systems (IPS)
-   Restricted management plane access (VPN, bastion hosts, zero-trust
    access)
-   File-level encryption for sensitive file transfers
-   Secure outbound controls (egress filtering, DNS control)
-   Strong workload identity (managed identities, workload federation)

## Controls Not Considered Strong (Baseline Only)

Do not count the following as strong controls:

-   TLS alone
-   Encryption at rest
-   Username/password without MFA
-   HMAC or digital signatures alone
-   Web Application Firewall (WAF)
-   Input validation and output encoding
-   RBAC alone
-   Intrusion Detection Systems (IDS)
-   API rate limiting
-   Secret storage alone
-   Password salting

These are assumed baseline hygiene.

## Required Output Table Format

Flow ID \| From \| To \| STRIDE Threats \| DREAD Risk Summary \|
Controls on Diagram \| Risk with Current Controls \| Recommended
Controls \| Risk with Recommended Controls

### Column Guidance

-   Flow ID: Unique identifier (F1, F2, etc.)
-   From / To: Explicit components or actors
-   STRIDE Threats: Only threats relevant to that traversal
-   DREAD Risk Summary: Brief qualitative assessment (High/Medium/Low +
    short justification)
-   Controls on Diagram: Only controls explicitly shown
-   Risk with Current Controls: Residual risk level
-   Recommended Controls: Minimum two strong controls
-   Risk with Recommended Controls: Updated residual risk

## Additional Reuse Guidance

-   Define system boundaries first.
-   Treat managed services as trust boundary transitions unless proven
    otherwise.
-   Treat third-party SaaS as hostile external trust zones.
-   Separate management plane from data plane.
-   Treat CI/CD pipelines as independent trust domains.
-   If sensitive data classification is not defined, assume worst-case
    sensitivity.
-   Document assumptions explicitly.

This template is stack-neutral and reusable across cloud, hybrid, or
on-prem architectures.
