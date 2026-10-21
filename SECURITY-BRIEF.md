# Pallets Security Advisory Brief

Compiled from live GitHub data for the three core Pallets projects: **Flask**, **Werkzeug**, and **Jinja**.

**Scope and method:** For each project, the official repository was located under the [Pallets](https://github.com/pallets) organization and its **repository security advisories** (the advisories published by the project itself on the repository's Security tab) were retrieved. These are project-published advisories, *not* Dependabot dependency alerts. Affected version ranges for the most severe advisories were confirmed against GitHub's global advisory database (`api.github.com/advisories`) using each GHSA id.

**Severity ranking used (highest to lowest):** critical > high > moderate > low.
Note: GitHub labels its middle severity tier "medium"; it is equivalent to "moderate" in the ranking above and is reported as returned by the API.

**Totals:** 18 published repository advisories across the three projects (Flask: 3, Werkzeug: 10, Jinja: 5).

---

## Flask

- **Repository:** `pallets/flask` — https://github.com/pallets/flask (The Python micro framework for building web applications.)
- **Advisory count:** 3
- **PyPI package:** `flask`

### Advisories (as returned)

| GHSA id | CVE | Severity | Summary |
| --- | --- | --- | --- |
| GHSA-m2qf-hxjv-5gpq | CVE-2023-30861 | high | Possible disclosure of permanent session cookie due to missing `Vary: Cookie` header |
| GHSA-4grg-w6v8-c28g | CVE-2025-47278 | low | Fallback key is used instead of current signing key |
| GHSA-68rp-wp8r-4726 | CVE-2026-27205 | low | Flask session does not add `Vary: Cookie` header when accessed in some ways |

### Most severe advisory

**GHSA-m2qf-hxjv-5gpq — CVE-2023-30861 — high** — Possible disclosure of permanent session cookie due to missing `Vary: Cookie` header. Vulnerable versions of Flask only set `Vary: Cookie` when the session is accessed or modified, not when it is refreshed without being accessed; a caching proxy may therefore cache and re-serve one client's session cookie to another client.

**Affected version ranges (from the GitHub global advisory database):**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/flask | >= 2.3.0, < 2.3.2 | 2.3.2 |
| pip/flask | < 2.2.5 | 2.2.5 |

---

## Werkzeug

- **Repository:** `pallets/werkzeug` — https://github.com/pallets/werkzeug (The comprehensive WSGI web application library.)
- **Advisory count:** 10
- **PyPI package:** `Werkzeug`

### Advisories (as returned)

| GHSA id | CVE | Severity | Summary |
| --- | --- | --- | --- |
| GHSA-xg9f-g7g7-2323 | CVE-2023-25577 | high | High resource usage when parsing multipart form data with many fields |
| GHSA-px8h-6qxv-m22q | CVE-2023-23934 | low | Cookie prefixed with `=` can shadow unprefixed cookie |
| GHSA-hrfv-mqp8-q5rw | CVE-2023-46136 | medium | High resource usage when parsing multipart/form-data containing a large part with CR/LF character at the beginning |
| GHSA-2g68-c3qc-8985 | CVE-2024-34069 | high | Werkzeug debugger vulnerable to remote execution when interacting with attacker controlled domain |
| GHSA-f9vj-2wh5-fj8j | CVE-2024-49766 | medium | Werkzeug `safe_join` not safe on Windows (UNC paths on Python < 3.11) |
| GHSA-q34m-jh98-gwm2 | CVE-2024-49767 | medium | Werkzeug possible resource exhaustion when parsing file data in forms |
| GHSA-hgf8-39gv-g3f2 | CVE-2025-66221 | medium | Werkzeug `safe_join()` allows Windows special device names |
| GHSA-87hc-h4r5-73f7 | CVE-2026-21860 | medium | Werkzeug `safe_join()` allows Windows special device names with compound extensions |
| GHSA-29vq-49wr-vm6x | CVE-2026-27199 | medium | Werkzeug `safe_join()` allows Windows special device names (multi-segment paths) |
| GHSA-g6x2-hccm-hh4m | CVE-2026-102598 | medium | Werkzeug `safe_join()` allows Windows special device names (empty ADS marker on NTFS) |

### Most severe advisory — tie (two advisories at high severity)

**1) GHSA-xg9f-g7g7-2323 — CVE-2023-25577 — high** — High resource usage when parsing multipart form data with many fields. The multipart form data parser parses an unlimited number of parts, allowing an attacker to cause denial of service (worker CPU/RAM/file-handle exhaustion).

**Affected version ranges (from the GitHub global advisory database):**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/Werkzeug | < 2.2.3 | 2.2.3 |

**2) GHSA-2g68-c3qc-8985 — CVE-2024-34069 — high** — Werkzeug debugger vulnerable to remote execution when interacting with attacker controlled domain. An attacker who gets a developer to interact with a domain they control and enter the debugger PIN can gain access to the debugger (and code execution) even when it only runs on localhost.

**Affected version ranges (from the GitHub global advisory database):**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/Werkzeug | < 3.0.3 | 3.0.3 |

---

## Jinja

- **Repository:** `pallets/jinja` — https://github.com/pallets/jinja (A very fast and expressive template engine.)
- **Advisory count:** 5
- **PyPI package:** `Jinja2`

### Advisories (as returned)

| GHSA id | CVE | Severity | Summary |
| --- | --- | --- | --- |
| GHSA-h5c8-rqwp-cp95 | CVE-2024-22195 | medium | HTML attribute injection when passing user input as keys to `xmlattr` filter |
| GHSA-h75v-3vvj-5mfj | CVE-2024-34064 | medium | Jinja vulnerable to HTML attribute injection when passing user input as keys to `xmlattr` filter |
| GHSA-gmj6-6f8f-6699 | CVE-2024-56201 | medium | Sandbox breakout through malicious filenames |
| GHSA-q2x7-8rv6-6q7h | CVE-2024-56326 | medium | Sandbox breakout through indirect reference to format method |
| GHSA-cpwx-vrp4-4pq7 | CVE-2025-27516 | medium | Sandbox breakout through `attr` filter selecting format method |

### Most severe advisory — five-way tie (all advisories are medium/moderate severity; all five are called out)

**1) GHSA-h5c8-rqwp-cp95 — CVE-2024-22195 — medium**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/jinja2 | < 3.1.3 | 3.1.3 |

**2) GHSA-h75v-3vvj-5mfj — CVE-2024-34064 — medium**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/Jinja2 | < 3.1.4 | 3.1.4 |

**3) GHSA-gmj6-6f8f-6699 — CVE-2024-56201 — medium**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/jinja2 | >= 3.0.0, <= 3.1.4 | 3.1.5 |

**4) GHSA-q2x7-8rv6-6q7h — CVE-2024-56326 — medium**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/jinja2 | <= 3.1.4 | 3.1.5 |

**5) GHSA-cpwx-vrp4-4pq7 — CVE-2025-27516 — medium**

| Package | Vulnerable version range | First patched version |
| --- | --- | --- |
| pip/Jinja2 | <= 3.1.5 | 3.1.6 |

---

## Most severe

Across all three projects, three advisories carry GitHub's **high** severity rating, all with CVSS 3.1 base score 7.5: Flask's GHSA-m2qf-hxjv-5gpq, and Werkzeug's GHSA-xg9f-g7g7-2323 and GHSA-2g68-c3qc-8985. No advisory for any of the three projects is rated critical. The single worst advisory is:

- **Repository:** `pallets/werkzeug`
- **GHSA id:** GHSA-2g68-c3qc-8985 (CVE-2024-34069)
- **Severity:** high (CVSS 3.1: 7.5, `CVSS:3.1/AV:N/AC:H/PR:N/UI:R/S:U/C:H/I:H/A:H`, CWE-352)
- **Summary:** Werkzeug debugger vulnerable to remote execution when interacting with attacker controlled domain — allows an attacker to execute code on a developer's machine if they can lure the developer to interact with an attacker-controlled domain/subdomain and enter the debugger PIN.
- **Affected versions (from the GitHub global advisory database):** `Werkzeug < 3.0.3` (pip); first patched version 3.0.3.

**Why this one:** All three high-rated advisories share the same CVSS base score (7.5), but GHSA-2g68-c3qc-8985 is the only one whose CVSS vector flags high impact across all three dimensions (confidentiality, integrity, and availability: `C:H/I:H/A:H`), and it is a remote code execution class issue on the developer's machine. The other two are single-dimension: CVE-2023-30861 is confidentiality-only (`C:H/I:N/A:N`) and CVE-2023-25577 is availability-only (`C:N/I:N/A:H`). For transparency in an audit record: severity-wise this is a three-way tie at "high"; the choice above is based on the CVSS impact profile.

---

*Sources: GitHub repository security advisories for `pallets/flask`, `pallets/werkzeug`, and `pallets/jinja` (Security tab, project-published), and the GitHub global advisory database (https://api.github.com/advisories) for affected version ranges, retrieved at the time this brief was compiled.*
