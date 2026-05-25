# Security Policy

## Supported versions

This tool is a single-file static web application. Only the current version in the `main` branch is maintained.

## Reporting a vulnerability

If you discover a security issue in this tool, please **do not open a public GitHub issue**.

Report it privately by emailing [info@bare-consult.com](mailto:info@bare-consult.com) with:

- A description of the vulnerability
- Steps to reproduce
- Potential impact

You will receive a response within 5 business days. If the issue is confirmed, a fix will be released as soon as reasonably practicable and you will be credited (unless you prefer otherwise).

## Scope

Given the tool's architecture — client-side only, no server, no authentication, no persistent storage — the realistic attack surface is limited to:

- Cross-site scripting (XSS) via user input
- Content Security Policy bypasses
- Malicious use of the Formspree lead capture endpoint

Out of scope: Formspree platform vulnerabilities (report those directly to Formspree), Google Fonts CDN issues, and GitHub Pages infrastructure.
