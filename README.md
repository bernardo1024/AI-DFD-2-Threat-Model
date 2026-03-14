# DFD Threat Model Master Prompt

## Overview

This repository contains a reusable, technology-agnostic master prompt
for performing structured threat modeling using a Data Flow Diagram
(DFD).

It standardizes: - Trust boundary analysis - STRIDE-based threat
identification - DREAD-based qualitative risk scoring - Strong security
control validation - Residual risk documentation

------------------------------------------------------------------------

## Purpose

The prompt is designed to:

1.  Force explicit trust boundary identification.
2.  Prevent weak controls from being treated as sufficient mitigation.
3.  Require minimum strong controls per boundary traversal.
4.  Produce structured output for security review and approval
    workflows.

------------------------------------------------------------------------

# How To Use Guide

## Step 1 -- Create a Proper DFD

Your DFD must include:

-   External actors
-   Application components
-   Datastores
-   Third-party integrations
-   Trust boundaries clearly drawn
-   Explicit data flow arrows
-   Sensitive data classification
-   Add security context notes/comments to diagram (TLS 1.3 used for all communications...)

If trust boundaries are not drawn, define them before running the
prompt.

------------------------------------------------------------------------

## Step 2 -- Customize the Prompt

In the master prompt file (Generic_DFD_Threat_Model_Master_Prompt.md):

1.  Replace the Tech Stack placeholders with your environment:
    -   Cloud provider
    -   Hosting model
    -   Runtime/language
    -   Identity provider
    -   Datastores
    -   Messaging/integration patterns
    -   External SaaS dependencies
2.  Replace the default sensitive data assumption (PHI) with your
    classification:
    -   PII
    -   PCI
    -   Confidential data
    -   Regulated financial data
    -   Trade secrets

------------------------------------------------------------------------

## Step 3 -- Provide Required Inputs

When using the prompt with an LLM, include:

-   The full DFD
-   The customized tech stack section
-   Any known security controls already implemented
-   Clarification of whether TLS is used everywhere

Important: TLS alone is treated as baseline and not a strong control.

------------------------------------------------------------------------

## Step 4 -- Review the Output Table

The model will produce a table in this format:

Flow ID \| From \| To \| STRIDE Threats \| DREAD Risk Summary \|
Controls on Diagram \| Risk with Current Controls \| Recommended
Controls \| Risk with Recommended Controls

You must:

-   Validate STRIDE coverage
-   Validate DREAD logic
-   Confirm strong controls are truly strong
-   Review residual risk
-   Identify design changes required

------------------------------------------------------------------------

## Step 5 -- Iterate

If residual risk remains High:

-   Adjust architecture
-   Add boundary controls
-   Reduce implicit trust
-   Re-run the prompt

Threat modeling is iterative.

------------------------------------------------------------------------

# Customization Patterns

## Multi-Cloud

Add explicit trust boundaries between: - Cloud providers - Identity
domains - Cross-cloud networking - Shared infrastructure layers

## Kubernetes

Treat as boundaries: - Namespaces - Clusters - Ingress controllers -
Service mesh - Workload identity domains

## Serverless

Treat as boundaries: - API gateway to function - Function to datastore -
Function to third-party APIs - IAM role assumptions

## CI/CD

Treat as independent trust domains: - Developer → Repo - Repo →
Pipeline - Pipeline → Artifact Registry - Pipeline → Production -
Registry → Runtime

------------------------------------------------------------------------

# Strong Control Philosophy

The prompt separates:

Baseline Controls (expected hygiene) vs. Strong Controls (boundary-grade
controls)

Baseline controls include: - TLS - Encryption at rest - WAF - RBAC
alone - Rate limiting

Strong controls include: - mTLS - Network segmentation - Least privilege
IAM - MFA - Private connectivity - IPS - Strong session controls -
Scoped tokens - Centralized identity enforcement

Boundary crossings require strong controls.

------------------------------------------------------------------------

# Recommended Workflow

1.  Architecture design completed
2.  DFD created with trust boundaries
3.  Prompt customized
4.  Threat model generated
5.  Engineering design updated
6.  Residual risk reviewed
7.  Security sign-off documented

------------------------------------------------------------------------

# Governance and Versioning

When updating the master prompt:

-   Maintain trust boundary focus
-   Preserve strong vs baseline distinction
-   Keep output table format stable
-   Document changes in this README

------------------------------------------------------------------------

# Expected Outcomes

Consistent use of this prompt should:

-   Reduce implicit trust in designs
-   Increase architectural rigor
-   Improve security review quality
-   Improve documentation clarity
-   Standardize risk discussions
-   Accelerate security approvals

------------------------------------------------------------------------

# Disclaimer

This prompt accelerates structured threat modeling. It does not replace
formal risk assessment programs or compliance frameworks.
