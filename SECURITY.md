# Security Policy

## Reporting a Vulnerability

**Please do not open a public GitHub issue for security vulnerabilities.**

To report a vulnerability, use one of these channels:

- **GitHub private disclosure:** Use the [Security tab](https://github.com/TadMSTR/grafana-dashboards/security/advisories/new) to submit a private advisory.
- **Email:** Send a description to `security.i9v75@8alias.com` with the subject line `[grafana-dashboards] Security Report`.

Include as much detail as possible: the affected component, steps to reproduce, and potential impact.

## Scope

**In scope:**

- Dashboard or variable configurations that embed credentials or sensitive infrastructure details
- Data source configurations that bypass intended permission boundaries
- Provisioning configs that expose internal service topology to unintended audiences

**Out of scope:**

- Vulnerabilities in Grafana itself or the underlying data sources
- Issues that require attacker control of the Grafana instance or provisioning directory
- Theoretical weaknesses without a realistic attack path

## Response Expectations

| Stage | Timeline |
|-------|----------|
| Acknowledgement | Within 3 business days |
| Initial assessment | Within 7 business days |
| Fix or remediation plan | Within 30 days for critical/high; 60 days for medium/low |

This is a personal project maintained by one developer. Response times are best-effort.
If you haven't heard back within 3 business days, a follow-up email is welcome.

## Disclosure

Coordinated disclosure is preferred. Please allow time for a fix to be released before
public disclosure. The CHANGELOG documents remediated findings at an appropriate level
of detail after each release.
