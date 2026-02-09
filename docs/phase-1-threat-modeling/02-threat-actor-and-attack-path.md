# Phase 1.2 – Threat Actor & Attack Path

## Threat Actor Profile
- Skill level: Medium
- Motivation: Credential access and internal reconnaissance
- Operational style: Low-noise, short attack window

## Initial Access Vector
- Entry point: Public-facing web server
- Why this vector is realistic:
  - Exposed service reachable from the internet
  - Common target for automated and semi-targeted attacks

## Attack Path (Kill Chain)
1. Initial Access:
   - Unauthorized access attempt against the web server
2. Execution:
   - Execution of commands or scripts on the compromised host
3. Persistence:
   - Temporary persistence via scheduled task or user account
4. Privilege Escalation:
   - Abuse of misconfigured permissions or credentials
5. Lateral Movement:
   - Access to internal services or log infrastructure
6. Objective:
   - Credential harvesting and environment mapping

## Constraints & Assumptions
- No zero-day exploits
- No physical access
- Attack duration is limited to minutes, not days

