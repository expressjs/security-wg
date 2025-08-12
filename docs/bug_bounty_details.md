# Bug Bounty Details

> [!NOTE]  
> This file is a version-controlled copy of the official policy on [YesWeHack](https://yeswehack.com/business-units/sovereign-tech-fund/programs/express-js-bug-bounty-program).
It is used internally to track changes and coordinate updates.
**Do not rely on this file as the source of truth when reporting vulnerabilities. Always refer to the official YesWeHack page to ensure you have the latest and most accurate information**.

----


### Bug bounty description

| Scope Type   |      Scope      |  Asset value |
|----------|:-------------:|------:|
| Other |  npm: express | high |
| Other |  npm: body-parser | high |
| Other |  npm: path-to-regexp | high |
| Other |  npm: cookie | high |
| Other |  npm: http-errors | high |
| Other |  npm: on-finished | high |
| Other |  npm: multer | high |


### Out-Of-Scope
- Anything related to https://express.com is out of scope.
- npm packages that are not explicitly listed in the scope of the program are not accepted.


## Qualifying Vulnerabilities
- Issues found in outdated or unsupported versions of our npm packages are not accepted.
- For examples and guidance, see: https://expressjs.com/en/advanced/security-updates.html


## Non-Qualifying Vulnerabilities

- Anything not listed under Qualifying Vulnerabilities is not accepted by default and may only be considered at the discretion of the maintainers.
- Reports describing purely hypothetical vulnerabilities without a reproducible proof of concept.
- Proofs of concept that do not use publicly available or freely accessible software.
- Issues found in external dependencies, including cryptographic libraries.
- Issues discovered through oss-fuzz or other upstream CI systems.
- Reports generated solely by AI tools.
- Reports concerning vulnerabilities in example code included in the repositories.
- For reference examples, see: https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md#examples-of-non-vulnerabilities


## Policy

---

⚠️ **Your report must contain all the mandatory parts of the report submission template proposed on this program**⚠️

# Project


Express.js is a fast, unopinionated, minimalist web framework for Node.js. It provides a robust set of features for building web and mobile applications. Express handles routing, middleware, and HTTP utilities, serving as a foundational framework in the Node.js ecosystem.

The scope of this program spans multiple npm packages maintained by the Express.js team across three GitHub organizations ([expressjs](https://github.com/expressjs), [pillarjs](https://github.com/pillarjs) and [jshttp](https://github.com/jshttp)). These repositories contain the core modules, middleware components, and foundational utilities that power the Express.js ecosystem. 

This bug bounty program is paid for by the [Sovereign Tech Resilience program](https://www.sovereigntechfund.de/programs/bug-resilience).

## Scopes

You can find our repositories on three different GitHub organizations ([expressjs](https://github.com/expressjs), [pillarjs](https://github.com/pillarjs) and [jshttp](https://github.com/jshttp)).

You can find the packages in npm: [express](https://www.npmjs.com/package/express), [body-parser](https://www.npmjs.com/package/body-parser), [path-to-regexp](https://www.npmjs.com/package/path-to-regexp), [cookie](https://www.npmjs.com/package/cookie), [http-errors](https://www.npmjs.com/package/http-errors), [on-finished](https://www.npmjs.com/package/on-finished) and [multer](https://www.npmjs.com/package/multer)

## Program Rules

- We welcome external reviews by security researchers in order to identify bugs in our components.
- The scope of this program only applies to the software we build, not to our CI infrastructure or our git/website hosting, and any such attack is prohibited.
- Issues must be reproducible in our setup in order to be accepted as valid.
- We operate this bounty program on a "One Fix One Reward" basis. We consider an issue duplicated if it was previously reported through other channels, and also if it affects a common code module and it was already reported for a different component.
- The Express.js project includes a variety of tools and components, many of which are independent modules, and some of which are experimental. This bug bounty program covers only a specific subset of these components, which will be explicitly defined in the scope section. The list of included components may change over time as the project evolves.
- Express.js takes an unopinionated approach to application design and security configuration. Many features are optional and intentionally flexible to accommodate a wide range of use cases. For this reason, not all security-related behaviors are enforced by default. To better understand what constitutes a valid security vulnerability within our ecosystem, please refer to the [Express Threat Model](https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md). This document outlines what Express considers in scope for security concerns and may be updated over time as the framework and its environment evolve.

### Precautions

- Do not include Personally Identifiable Information (PII) in your report and redact or obfuscate any PII that is part of your PoC (logs, screenshot, terminal captures, etc.).

## Eligibility

Every valid report that helps us improve the security of the project is welcome, however, in order to qualify for monetary rewards the following eligibility requirements must be met at a minimum:

- The issue must originate from code published on npm, within a version of an npm package that falls under the scope of this program.
- The vulnerability must be previously undisclosed, both publicly and privately, and must not have been reported through any other channel ([security policy](https://github.com/expressjs/.github/blob/master/SECURITY.md)).
- The issue must meet the qualifying criteria defined in the program’s scope and threat model.
- The report must include a working reproducer (e.g., code, configuration, or sequence of steps) that demonstrates the issue clearly and reliably.
- You must not be a current [Express.js TC (Technical Committee) member](https://github.com/expressjs/express#tc-technical-committee), an active contributor listed in the project governance documents ([reference](https://github.com/expressjs/discussions/blob/master/docs/contributing/captains_and_committers.md)) - excluded triage and documentation (website) teams, or affiliated with any team listed in the Security WG ([ref](https://github.com/expressjs/security-wg#members)).
- Severity is assessed based on the maximum impact demonstrated by your proof of concept (PoC), not on hypothetical impact.
- Only issues affecting released npm packages are eligible. Vulnerabilities found in unreleased code, git branches, or forks are not eligible for rewards.
- **Your report must contain all the mandatory parts of the report submission template proposed on this program**



## Rating and Responsible Disclosure

CVSS is used to rate and categorize vulnerabilities. Vulnerabilities will be publicly disclosed after sufficient time has passed and fixes have been backported where needed, if deemed necessary in coordination with other maintainers.

Advisories will be published on the advisory page of our GitHub repository, and where deemed necessary as CVEs.

We handle the full disclosure process and expect submitters not to disclose any findings themselves. If requested, we will fully credit the reporters in the advisories.

The process for external reporting is described on GitHub

---