# Custodia

> *Latin* **custōdia**, "guardianship; safekeeping; custody".

A working **fork-and-extension** of the [GRC Engineering Club](https://grcengclub.com)'s open-source GRC toolkit, [`claude-grc-engineering`](https://github.com/GRCEngClub/claude-grc-engineering), maintained personally by **[Devam Shah](https://github.com/DevamShah)**.

This repository tracks every plugin the upstream community ships, plus original contributions authored personally by Devam — most of which have now landed in upstream `main`.

For the upstream project's own README (the project description, plugin catalogue, and contribution conventions), see [`UPSTREAM-README.md`](UPSTREAM-README.md).

---

## The problem Custodia exists to solve

A working privacy and security programme has to compose three layers correctly:

1. **A statutory baseline** — DPDPA in India, GDPR in the EU, SOC 2 / FedRAMP / NIST in the US, PCI for cardholder data, HIPAA for health.
2. **Sectoral overlays** — RBI, SEBI, IRDAI, DoT/TRAI for Indian regulated entities. State banking regulators. Health authorities. Telecom regulators. Each adding privacy- and security-adjacent obligations on top of the statute.
3. **Engineering reality** — cloud, vendors, sub-processors, identity, log retention, model training, consent capture, withdrawal cascades, deletion plumbing.

Off-the-shelf compliance content covers (1) at a textbook level and ignores (2) and (3). Sectoral playbooks cover (2) for one vertical and ignore (1) and (3). Cloud configuration tools cover (3) and ignore (1) and (2). The result is the same in every organisation: practitioners spend most of their time **re-stitching the same three layers** for their own context, by hand.

**Custodia is the stitched workbook.** It runs in Claude Code — already where the engineering work happens — and joins all three layers into a single tool. The upstream `claude-grc-engineering` provides the framework-plugin pattern, the SCF crosswalk backbone, and the broad framework coverage. Custodia adds India-specific extensions and engineering-grade content for layers (2) and (3) that off-the-shelf material misses.

The bet: practitioners shouldn't have to re-stitch every quarter. The toolkit ships, the community improves it, every CISO benefits.

## What's in this repository

This is a fork — every plugin the GRC Engineering Club ships lives here, including SOC 2, NIST 800-53, ISO 27001, FedRAMP Rev 5, FedRAMP 20X, PCI DSS, CMMC, HITRUST, CIS Controls, GDPR, CSA CCM, NYDFS, DORA, StateRAMP, Essential 8, GLBA, US Export Controls, PBMM, ISMAP, IRAP, Singapore PDPA, Cyber Essentials Plus (Danzell), and the **India DPDPA plugin authored personally by Devam**. Plus the persona plugins (`grc-engineer`, `grc-auditor`, `grc-internal`, `grc-reporter`, `grc-tprm`), the connectors (`aws-inspector`, `gcp-inspector`, `github-inspector`, `okta-inspector`), the OSCAL toolchain, and the new `teach-me` plugin.

Run `/grc-engineer:frameworks` from a Claude Code session that has Custodia installed to discover everything live.

## Devam's contributions to upstream

| PR | Title | Status |
|---|---|---|
| [#70](https://github.com/GRCEngClub/claude-grc-engineering/pull/70) | `fix(plugins): use object form for plugin.json author field` | Closed (folded into #71) |
| [#71](https://github.com/GRCEngClub/claude-grc-engineering/pull/71) | `ci(plugins): validate manifests against JSON Schema on every PR` | **Merged** by [@ethanolivertroy](https://github.com/ethanolivertroy) on 2026-04-26 |
| [#72](https://github.com/GRCEngClub/claude-grc-engineering/pull/72) | `feat(frameworks): Reference-depth India DPDPA plugin (ind-dpdpa)` | **Merged** by [@ethanolivertroy](https://github.com/ethanolivertroy) on 2026-04-26 |

All three contributions are now part of the upstream community toolkit. The India DPDPA plugin in particular handles the parallel-clock breach-notification problem (DPDPA 72 h running alongside CERT-In 6 h, RBI 6 h, SEBI 6 h, IRDAI per current direction, DoT/TRAI per Telecom Cyber Security Rules 2024) that most regulated Indian Fiduciaries miss.

## Install

### Use the upstream Club edition (recommended)

Now that everything has landed upstream, the simplest path is to install directly from the GRC Engineering Club:

```bash
# In Claude Code
/plugin marketplace add GRCEngClub/claude-grc-engineering
/plugin install grc-engineer@grc-engineering-suite     # the engineering hub
/plugin install ind-dpdpa@grc-engineering-suite        # India DPDPA, Devam's contribution
/plugin install soc2@grc-engineering-suite             # SOC 2
# ...any other plugin
```

### Or use Custodia (this repo)

Custodia tracks upstream `main`. If you'd prefer to install from this fork — for example, to track Devam's pre-upstream branches as he develops new plugins — use:

```bash
/plugin marketplace add DevamShah/custodia
/plugin install ind-dpdpa@grc-engineering-suite
```

(The marketplace identifier stays `grc-engineering-suite` because Custodia is a fork that hasn't renamed it.)

## India DPDPA plugin

`plugins/frameworks/ind-dpdpa/` ships:

- **`/ind-dpdpa:scope`** — territorial / material applicability, role assignment (Data Fiduciary / Processor / Consent Manager), Significant Data Fiduciary trigger walkthrough, cross-border posture, sectoral overlay detection, children's-data trigger.
- **`/ind-dpdpa:assess`** — gap assessment via SCF crosswalk (`apac-ind-dpdpa-2023`, 41 SCF → 96 framework controls).
- **`/ind-dpdpa:evidence-checklist`** — 14 obligation themes (Notice, Consent, Legitimate Uses, Purpose Limitation, Accuracy, Security, Breach, Retention, Principal Rights, Children, SDF, Cross-border, Consent Manager, Governance) with collection guidance and "what good looks like" criteria.
- **`/ind-dpdpa:breach-process`** — DPDPA 72-hour clock + parallel sectoral clocks (CERT-In 6 h, RBI 6 h, SEBI 6 h, IRDAI, DoT/TRAI), 5-phase playbook (detect → classify → notify → investigate → review).
- **`ind-dpdpa-expert` skill** — Reference-grade DPDPA knowledge available to Claude in any session where the plugin is installed.

See [`plugins/frameworks/ind-dpdpa/README.md`](plugins/frameworks/ind-dpdpa/README.md) for plugin documentation.

## Authorship

Custodia is created and maintained personally by **[Devam Shah](https://github.com/DevamShah)** — a CISO with deep DPDPA, RBI, SEBI, IRDAI, and Indian-sectoral-compliance experience. All work in this repository is on personal time, on personal infrastructure, and is **not affiliated with any employer**.

Upstream community attribution (the GRC Engineering Club, including co-leads [@ajy0127](https://github.com/ajy0127) and [@ethanolivertroy](https://github.com/ethanolivertroy)) is preserved in [`UPSTREAM-README.md`](UPSTREAM-README.md), [`MAINTAINERS.md`](MAINTAINERS.md), and the per-plugin metadata. The Club's Code of Conduct, governance, and CC BY-ND 4.0 SCF attribution all carry through to this fork.

## License

[MIT](LICENSE) for original code, copyright © 2026 GRC Engineering Club contributors and Devam Shah. Exceptions documented in [`LICENSE`](LICENSE) (one plugin is CC BY-SA 4.0 per upstream terms; SCF data is CC BY-ND 4.0 and consumed via API call, not redistributed).

## Disclaimer

Custodia and every plugin within it are **engineering and assessment guidance only**. They are **not legal advice**. Confirm postures with qualified counsel before treating any output as definitive. For statutory enforcement and binding interpretation:

- **DPDPA** — Data Protection Board of India (DPB) under MeitY.
- **GDPR / UK GDPR** — your relevant EU / UK supervisory authority.
- **Sectoral rules** — RBI / SEBI / IRDAI / DoT / TRAI / NHA / NCIIPC / CERT-In, per their own circulars and orders.

## Acknowledgements

- **[GRC Engineering Club](https://grcengclub.com)** — for the framework-plugin pattern, the broader OSS GRC suite, and the community ethos this fork extends. Co-leads [@ajy0127](https://github.com/ajy0127) and [@ethanolivertroy](https://github.com/ethanolivertroy). Special thanks to [@ethanolivertroy](https://github.com/ethanolivertroy) for the maintainer-edit pass that fixed four substantive blockers on the India DPDPA plugin (version baseline, Section 15 ₹10,000 / ₹50 crore correction, and the Section 2(u) paraphrase) before merging — generous engagement that made Devam's contribution materially better.
- **[@AnandSundar](https://github.com/AnandSundar)** — for the original Stub PR ([#66](https://github.com/GRCEngClub/claude-grc-engineering/pull/66)) that locked in the SCF metadata baseline (`apac-ind-dpdpa-2023`) the Reference upgrade was built on.
- **[Secure Controls Framework](https://securecontrolsframework.com)** — the canonical control vocabulary backing every gap assessment.
- **DPDPA drafters and the Indian privacy community** — whose work the plugin tries to make operational.
