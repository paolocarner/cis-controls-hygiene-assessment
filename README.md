# CIS Controls Hygiene Assessment

A free, client-side self-assessment tool that guides organisations through 20 curated safeguards from CIS Controls v8.1 Implementation Group 1 (IG1) — the hygiene baseline of the [Cybersecurity Investment Pyramid](https://paolocarner.com/blog/just-show-me-the-risk-first-why-this-common-executive-push-back-misses-the-point) (Verslegers & Bobbert, 2024).

Built and maintained by [Paolo Carner](https://paolocarner.com).

---

## What it does

The tool runs a paginated self-assessment — one safeguard at a time — and produces a prioritised gap list with a hygiene score.

**Assessment phase**

- 20 curated IG1 safeguards across CIS Controls 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 14, and 17
- Three answer states per safeguard: Yes, fully / Partially / No or Unsure
- Each safeguard includes a plain-language rationale (why it matters) and a concrete first action

**Results phase**

- Animated hygiene score (0–100), colour-coded by band
- Priority gap list ordered by `impact × (6 − effort)` — high impact, quick wins surface first
- Each gap shows impact and effort badges and a recommended first action
- Investment Pyramid position indicator with contextual interpretation
- "Controls in place" list for positive reinforcement
- Optional PDF report via email (Formspree lead capture)
- Calendly CTA for prospects who want an expert review

---

## Safeguard selection rationale

20 safeguards selected from the 56 IG1 safeguards in CIS Controls v8.1, cross-referenced against:

- Verizon DBIR root-cause distribution (credential abuse, unpatched systems, missing logging, misconfiguration)
- CIS Controls v8.1 IG1 safeguard list
- Blog framing: MFA, patching, asset inventory, logging, and hardening as the hygiene exemplars

Controls covered: CIS 1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 14, 17.

---

## Scoring

| Field | Formula |
|---|---|
| **Priority score** | `impact × (6 − effort)` |
| **Max priority** | 25 (impact 5, effort 1) |
| **Hygiene score** | Yes = 1.0, Partial = 0.5, No = 0.0 — as % of max |

Higher priority score = fix this first.

---

## Architecture

Single HTML file — no framework, no build step, no dependencies beyond Google Fonts.

| Concern | Approach |
|---|---|
| Fonts | DM Sans + DM Mono via Google Fonts |
| Lead capture | Formspree (JSON POST) |
| Booking | Calendly link |
| Storage | None — no localStorage, no cookies, no tracking |
| Deployment | GitHub Pages |

---

## Deployment

The tool is a single `index.html` file deployed via GitHub Pages from the root of the repository.

1. Fork the repository
2. Enable GitHub Pages: **Settings → Pages → Deploy from branch → main → / (root)**
3. Update the Formspree endpoint in the `btnSendPdf` event listener with your own form ID
4. Update the Calendly URL and contact email if needed

### Lead capture setup (Formspree)

1. Create a free account at [formspree.io](https://formspree.io)
2. Create a new form and copy the form ID
3. Replace `mlgpjnjz` in the `btnSendPdf` listener with your form ID
4. Submit a test from the live GitHub Pages URL to confirm the endpoint

> **Note:** Formspree will return a CORS error when tested from `file://` locally. This is expected behaviour — it is not a bug. Test from the deployed GitHub Pages URL only.

Fields submitted: `email`, `hygiene_score`, `gaps_count`, `gap_summary`, `tool` tag, `_subject`.

---

## Limitations

- **Self-reported answers only.** Results reflect stated posture, not verified posture. This tool is a screening indicator, not a certified assessment.
- **IG1 is the floor, not the ceiling.** Many organisations will need IG2 and IG3 controls. This tool covers the minimum viable hygiene baseline only.
- **PDF is a lead capture, not a generated document.** The "send my report" feature submits the gap summary to Formspree, which triggers a follow-up. Client-side PDF generation is not implemented.
- **Priority scores are indicative.** Impact and effort weights are expert-calibrated but not organisation-specific. A qualified advisor should validate priorities in context.
- **CIS Controls v8.1 (June 2024).** The safeguard list reflects v8.1. Review annually for updates.

---

## Security notes

- All user input escaped via `escapeHtml()` before DOM insertion — no raw user data injected as HTML
- No `eval()` or `innerHTML` with user-controlled content
- All interactive elements wired via `addEventListener` after injection, never inline `onclick`
- External links opened with `noopener noreferrer`
- No localStorage, sessionStorage, or cookies
- Content Security Policy meta tag included

---

## Related

- [NIS2 Applicability Self-Assessment](https://github.com/paolocarner/nis2-applicability) — determine whether NIS2 applies to your organisation
- [NIS2 SME Toolkit](https://github.com/paolocarner/nis2-sme-toolkit) — free templates, checklists, and guidance
- [Why "show me the risk first" misses the point](https://paolocarner.com/blog/just-show-me-the-risk-first-why-this-common-executive-push-back-misses-the-point) — the thinking behind this tool

---

## Disclaimer

This tool is a self-reported screening aid only. It is not legal or professional advice and does not constitute a certified compliance or security determination. Always engage qualified security professionals before acting on these results.

---

## Licence

[CC BY-NC 4.0](LICENSE) — free to share and adapt with attribution, no commercial use without permission.

---

## Contributions

This repository is not actively seeking contributions. If you spot an error or have a substantive suggestion, open an issue or email [info@bare-consult.com](mailto:info@bare-consult.com).
