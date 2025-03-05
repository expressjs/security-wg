# Security Report Handling Process
**Version:** 1.0  
**Last Updated:** March 2025  
**Maintainers:** Security Triage Team  

## Introduction
Security is a top priority for the Express.js project. This document outlines the **formal process** for handling **security reports**, including how to **triage**, **assess**, and **disclose** vulnerabilities responsibly.

## Scope

The Security Triage Team will use this document as a process guide when a security vulnerability is reported, from triage to resolution. This process must align with the project's [SECURITY policy](https://github.com/expressjs/.github/blob/master/SECURITY.md) and cannot diverge significantly.


## Security Report Handling Flowchart
The following diagram details the **decision-making process** for handling security reports:

```mermaid
flowchart TD
    A[Security Report Received] --> B[Assign Security Report Coordinator]
    B --> E{Premature Disclosure?}
    
    E -- No --> J[Proceed with Standard Private Process]
    E -- Yes --> F[Privatize Disclosure]
    F --> G[Handle Related PRs & Issues]
    G --> H[Request GitHub to Remove Public PR/Issues]
    H --> I[Create Public Placeholder Issue]
    I --> J[Acknowledge within 5 days to the Reporter]
    J --> K[Create Issue in Triage Repo for Visibility]

    K --> L[Assess Report]
    L --> M{Enough Information?}
    
    M -- No --> N[Request Additional Info]
    N --> L[Assess Report]
    
    M -- Yes --> O{Valid Vulnerability?}
    O -- No --> X[Close Report as Invalid]
    X --> Y[Acknowledge within 10 days to the Reporter]
    
    O -- Yes --> Q[Create Advisory]
    Q --> Q1[Calculate CVSS Score]
    Q1 --> Q2[Request a CVE]

    Q2 --> R{Patch Required?}
    
    R -- No --> Z[Public Disclosure]
    
    R -- Yes --> T[Develop Patch]
    T --> U[Test Solution]
    U --> V[Add Regression Testing]
    V --> W[Create a Security Release with CVE Included]
    W --> Z[Public Disclosure]
    Z --> Z1[Notify Community]
    Z1 --> Z2[Official Blog Post]
    Z1 --> Z3[Social Media Announcements]
```
