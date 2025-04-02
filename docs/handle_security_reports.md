# Security Report Handling Process
**Version:** 1.0  
**Last Updated:** March 2025  
**Maintainers:** Security Triage Team  

## Introduction
Security is a top priority for the Express project. This document outlines the **formal process** for handling **security reports**, including how to **triage**, **assess**, and **disclose** vulnerabilities responsibly.

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

## Roles & Responsibilities

### Reporter

This person submits a security report to the Security Triage Team and provides detailed information about the suspected vulnerability. It is expected that the reporter will cooperate with the Security Triage Team during this process and follows responsible disclosure guidelines.

**Responsibilities**
- Submit a security report to the Security Triage Team.

**Expectations**
- Provide detailed information about the suspected vulnerability.
- Follow responsible disclosure guidelines (report privately before public disclosure).
- Cooperate with the security team by providing additional details when needed.
- Test and verify patches (when applicable).
- Respect security timelines and avoid premature public disclosure.

### Coordinator


This person acts the focal point for an specific security report and ensures the report follows all responsible disclosure guidelines, also coordinates the remediation process if a vulnerability is confirmed. The SRC ensures that the security report follows the process and coordinates necessary actions, but does not perform analysis, remediation, or patching themselves.

**Responsibilities**
- Acknowledge receipt of security reports within the required timeframe.
- Assign an Analyst to assess and validate the report.
- Ensure communication with the reporter throughout the process.
- Coordinate the remediation process if a vulnerability is confirmed.
- Oversee the advisory & CVE request process if applicable.
- Escalate critical vulnerabilities when necessary.
- Track all security reports for visibility and reporting.

**Requirements**
- Must be a member of the Security Triage Team.


### Analyst

**Responsibilities**
- Determine if the reported issue is a real vulnerability, and is in within the scope of our [threat model](https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md)
- Validate proof-of-concept exploits
- Assess the security report and determine its severity (assist in CVSS).
- Validate the reported vulnerability against best practices.
- Identify potential mitigation strategies and workarounds.
- Prepare a report for the Security Report Coordinator.

### Remediation Developer

**Responsibilities**
- Develop a patch or solution based on the reported vulnerability.
- Ensure the patch follows best practices and is testable.
- Add test(s) to the existing test suite to confirm the vulnerability (pre-patch) and confirm the fix (post-patch).
- Test the patch to ensure it works as expected.
- Create a pull request to merge the patch into the project.

## Runbook

The following sections outline the **step-by-step process**, explaining each decision, scenario, and possible actions. In this guide we also include links that are private (limited to the security triage team), a general overview of the process in flowchart format can be found [here](#security-report-handling-flowchart).

### Step 0: Security Report Received

A security vulnerability report is received via [official channels](https://github.com/expressjs/.github/blob/master/SECURITY.md#reporting-a-bug) or otherwise (i.e. via third-party advisory services, blog post, social media, etc.).

Ideally, the report must contain **clear and detailed information** like (Affected versions, a small PoC/sample project demonstrating the issue, steps to reproduce, expected vs. actual behavior, potential impact...) but this might not be the case depending on the communication channel used. Later on we will try to collect this information and refine the report.

### Step 1: Assign Security Report Coordinator (SRC) and consolidate the report

1.1 One person from the Security Triage Team will volunteer and self-assign to oversee the case. It is expected that the person will remain assigned until the end of the process, so they effectively take the role of [the Security Report Coordinator (SRC)](#security-report-coordinator-src).

1.2 If the report was created accidentally or intentionally in a public channel (e.g. GitHub issues), it is important to share this information ASAP in the private slack channel `#express-security-triage` so the Security triage team is aware of it. At this stage, our priority is to remove the report from public view as soon as possible and let the reporter know what happened next.

1.2.1 In the case of a report made public in a Pull request or issue under the Express organizations ownership the following process will be followed (by an Express TC member):

    * Move the issue to the private repository called [expressjs/security-triage](https://github.com/expressjs/security-triage).
    * For any related pull requests, create an associated issue in [expressjs/security-triage](https://github.com/expressjs/security-triage) repository.  Add a copy of the patch for the pull request to the issue. Add screenshots of discussion from the pull request to the issue.
    * [Open a ticket with GitHub](https://support.github.com/contact) to delete the pull request using Expressjs (team) as the account organization.
    * Open a new issue in the public repository with the title `FYI - pull request deleted #YYYY`. Include an explanation for the user:
        > FYI @xxxx we asked GitHub to delete your pull request while we work on releases in private.
    * Update the team in the slack channel #express-security-triage`.

1.2.2 In the case that the report is made public in a different channel that we don't own/control, the TC will attempt to mitigate this by trying to remove the report from public view (reporting to support, asking the reporter to remove the report, etc...).


1.3 At this stage the Security Report Coordinator (SRC) will create a (private) issue in [expressjs/security-triage](https://github.com/expressjs/security-triage) repository with the existing information from the security report (example: [expressjs/security-triage#14](https://github.com/expressjs/security-triage/issues/14)) unless it already exists (step 1.2.1). This issue will serve as the central discussion point for this particular report. At this stage is expected from the Security Report Coordinator (SRC) to acknowledge receipt of the security report to the reporter.

> [!Note]
> It is expected that the issue will be assigned to the Security Report Coordinator (SRC) and will remain open until the end of the process.

### Step 2: Review the Report and determine its severity

2.1 It is expected from the security triage team to review the report and determine its severity, also evaluating the impact on the project(s). In some cases the report might be too vague to properly determine its severity. In this case the Security Report Coordinator (SRC) will need to reach out to the reporter for more information and refine the report.

2.2 At this stage we are capable of determining the severity of the report based on the information provided and also if the report is still relevant. In case that the team has considered the report to be irrelevant or not valid, the Security Report Coordinator (SRC) will need to close the issue and inform the reporter that the report has been dismissed, ideally we can provide a reason for dismissal to prevent the report from being resubmitted within the project(s) in the future.

2.3 If the report is considered relevant and valid, the Security Report Coordinator (SRC) will create an advisory and request a CVE number. The Security Report Coordinator (SRC) will also include the remediation developer(s), analyst(s) and potentially the reporter in the advisory, so they can start to work on private fork to fix the security issue (example: [GHSA-qw6h-vgh9-j6wx](https://github.com/expressjs/express/security/advisories/GHSA-qw6h-vgh9-j6wx)).

### Step 3: Patch and release

3.1 The security triage team will determine if this vulnerability will be patched and work on it. In case that the vulnerability won't be patched jump to step 4.

3.2 The mitigation team (remediation developer(s), analyst(s), reporter(s)) will work on the patch(es), re-evaluate the report once the patch is ready and include regression tests (when possible).

3.3 The Express TC will announce publicly (social media and public issues) that there is security path available and the plan to do a release with an specific date (ideally) and the versions affected without providing additional information to prevent early disclosure.

3.4 The security triage, along with the repo captain(s) and the TC team, will create the releases and publish them to npm. In some cases one vulnerability can affect multiple packages requiring several coordinated releases.


### Step 4: Public disclosure

4.1 At this stage the Security Report Coordinator (SRC) will make the advisory public and close the coordination issue (opened in step 1).

4.2 The Security Report Coordinator (SRC) will also help to publish a blog post about the vulnerability and the patch (if applicable, example [September 2024 Security Releases](https://expressjs.com/2024/09/29/security-releases.html)).

4.3 The TC team will do social media announcements about the vulnerability and the patch (if applicable, example [Tweet post](https://x.com/UseExpressJS/status/1772300472730198037)).
