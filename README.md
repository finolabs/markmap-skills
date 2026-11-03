<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/icon-dark.svg">
    <img src="assets/icon.svg" width="96" height="96" alt="markmap-skills icon">
  </picture>
</p>

<h1 align="center">markmap-skills</h1>

<p align="center">
  <b>Create structured Markmap mindmaps with your AI agent.</b><br>
  Structured branches · Folding and decision tracking · Editable Markdown and interactive HTML.
</p>

<p align="center">
  <a href="https://github.com/finolabs/markmap-skills/actions/workflows/ci.yml"><img src="https://github.com/finolabs/markmap-skills/actions/workflows/ci.yml/badge.svg" alt="CI Status" /></a>
  <a href="https://github.com/finolabs/markmap-skills"><img src="https://img.shields.io/badge/Packaging-Checked-7FE2CE?logo=anthropic&logoColor=0B0B17" alt="Packaging checked locally" /></a>
  <a href="https://github.com/finolabs/markmap-skills"><img src="https://img.shields.io/badge/Runtime-Zero--Daemon-9750C4" alt="Zero Daemon" /></a>
  <a href="https://github.com/finolabs/markmap-skills"><img src="https://img.shields.io/badge/Agents-Claude%20%7C%20Codex%20%7C%20Antigravity-18181b" alt="Agent Support" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License: MIT" /></a>
  <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome" /></a>
</p>

---

## ⚡ What It Does

`markmap-skills` turns task-authorized notes and documents into editable Markdown and interactive Markmap HTML. Its instructions guide branch grouping, concise labels, folding, and decision tracking. Review generated content against your source before relying on it.

### Outputs and Requirements

| Output or behavior | Requirements and limits |
|---|---|
| **Editable Markdown** | Generated within the host agent; content accuracy requires review. |
| **Compiled HTML** | Uses Node.js/npx and pinned `markmap-cli`; initial compilation may download packages from npm. Libraries are embedded for offline viewing. |
| **CDN template HTML** | Loads pinned libraries from jsDelivr and requires internet access. Source labels render as plain text. |
| **Branch structure** | Instructions target 4–7 main branches, depth 3–4, and concise labels; these are generation guidelines rather than measured guarantees. |
| **Runtime** | No bundled MCP server or maintainer daemon. Host processing and token use depend on the agent platform. |

---

## 🔍 Example Transformations

The examples below illustrate formatting, not benchmark results or comparisons with other products. Include only facts and decisions supported by the input.

| Scenario | Source material | Mindmap representation |
|---|---|---|
| **Gateway Architecture** | The gateway uses JWT with RSA signatures and an edge token bucket. Kong was rejected because of idle cost. | `- **Auth**: JWT with RSA signatures`<br>`- **Rate Limit**: Token bucket at edge`<br>`- ~~Kong Gateway: Idle cost~~` |
| **Branch Structure** | Notes describe ingress, compute, storage, and telemetry components. | Group nodes under those four categories; use `<!-- markmap: fold -->` for dense detail. |
| **Decision Tracking** | State snapshot serialization is complete. WebSocket reconnection backoff is pending. Low latency trades off against stale reads. | `- [x] State snapshot serialization`<br>`- [ ] WebSocket reconnection backoff`<br>`+ Low latency / - Stale read risk` |

---

## 📦 Quick Installation

### 1. Claude Code

#### Via the FINOLABS catalog (Recommended):
In your Claude Code terminal session:
```bash
claude plugin marketplace add finolabs/plugins
claude plugin install markmap-skills@finolabs
```
Invoke the skill directly in any conversation:
```text
/markmap-skills:markmap Create an architecture mindmap for this microservices system
```

> **Installed `markmap-skills@fioenix-plugins` or `mindmap-skills@fioenix-plugins`?** This repository no longer serves a marketplace of its own. Run `claude plugin uninstall markmap-skills@fioenix-plugins` and `claude plugin marketplace remove fioenix-plugins`, then install `markmap-skills@finolabs` as above. The command is `/markmap-skills:markmap`.

#### On Claude Desktop / Web UI:
1. Navigate to **Customize** → **Plugins** → **Add** → **Add marketplace** → **Add from a repository**.
2. Enter repository: `finolabs/plugins`.
3. In Discover, select **markmap-skills** and click **Add**.
4. Invoke in chat using `/markmap` or via the `+` menu.

#### Local Development / Manual Link:
```bash
claude plugin add ~/Projects/markmap-skills
```

---

### 2. OpenAI Codex

#### Via Skills CLI:
```bash
DISABLE_TELEMETRY=1 npx --yes skills@1.5.20 add finolabs/markmap-skills --skill markmap --agent codex --global
```

This installs the skill, not an approved OpenAI directory plugin. The Skills CLI normally reports install telemetry; this command opts out. [skills.sh listings](https://skills.sh/docs/faq) are driven by user installs with telemetry. No listing or OpenAI approval is claimed here.

#### OpenAI Directory Status — Submissions Paused:

As of 2026-10-23, the owner reports that the OpenAI submission portal displays: **"We are not accepting more skills-only submissions at this time."** Treat new skills-only submissions as unavailable through that portal. This is an intake restriction, not a rejection of this package after review; no reopening date is known.

**Project decision (2026-10-23): keep `markmap-skills` skills-only.** Continue using the Skills CLI and marketplace catalogs documented here. We will not add an MCP server solely to qualify for Directory submission. Reconsider MCP only when a validated user workflow needs server-backed capabilities independently of Marketplace access. See the [decision, evidence, and readiness limits](docs/openai-skills-readiness.md#current-submission-status-and-product-decision--2026-10-23).

Local packaging remains available for testing and a future eligible submission; building a ZIP does not mean OpenAI is accepting it:
```bash
python3 scripts/package_plugin.py /tmp/markmap-skills-0.1.4.zip
```
The ZIP uses the supported `.codex-plugin/plugin.json` layout and contains exactly one plugin root. It excludes development files and compatibility catalogs. Resume submission preparation only after confirming that [Platform Plugins](https://platform.openai.com/plugins) accepts the submitting organization and package type. Identity verification, scans, review, and publication are separate gates; local checks and historical readiness receipts do not establish approval.

This OpenAI package retains its Desktop-only declaration for the local Node.js/npx rendering workflow. If accepted and published in the Directory in the future, that declaration restricts installation to the ChatGPT desktop app and use to locally running threads. The CDN template does not remove this restriction. The declaration neither creates an OpenAI listing nor bypasses the current intake restriction. Direct skill installation through other distributions is unchanged.

#### Via the FINOLABS catalog (`finolabs`):
```bash
codex plugin marketplace add finolabs/plugins
codex plugin add markmap-skills@finolabs
```

Refresh the catalog with `codex plugin marketplace upgrade finolabs`, then run `codex plugin add markmap-skills@finolabs` again. Codex caches each plugin by the version in `.codex-plugin/plugin.json`.

**Installed from an older catalog?** This repository no longer serves one. Only if `codex plugin list` shows `markmap-skills@Finolabs`, `markmap-skills@agybird` or `markmap-skills@fioenix-plugins`, remove that plugin and its marketplace before adding `finolabs/plugins`; on macOS `Finolabs` and `finolabs` share one plugin cache folder, so installing from both overwrites the plugin:
```bash
codex plugin remove markmap-skills@Finolabs      # or the selector you installed
codex plugin marketplace remove Finolabs         # or agybird / fioenix-plugins
codex plugin marketplace add finolabs/plugins
codex plugin add markmap-skills@finolabs
```
To roll back, pin the last release that served its own catalog: `codex plugin marketplace add finolabs/markmap-skills --ref v0.1.4`. Check the command names against `codex plugin --help` for your version.

#### Via Agent Skills Directory:
```bash
# In a specific project
mkdir -p .agents/skills
cp -r ~/Projects/markmap-skills/skills/markmap .agents/skills/

# Or machine-global
mkdir -p ~/.agents/skills
ln -s ~/Projects/markmap-skills/skills/markmap ~/.agents/skills/markmap
```

---

### 3. Google Antigravity

#### As a plugin:
Antigravity resolves `plugin@marketplace` only for its official marketplace, so install from the repository URL:
```bash
agy plugin install https://github.com/finolabs/markmap-skills
```
Check it with `agy plugin list`. There is no catalog to upgrade from, so run the command again to pick up a new release.

#### Machine-Global:
```bash
mkdir -p ~/.gemini/config/skills
ln -s ~/Projects/markmap-skills/skills/markmap ~/.gemini/config/skills/markmap
```

#### Workspace-Local:
```bash
mkdir -p .agents/skills
cp -r ~/Projects/markmap-skills/skills/markmap .agents/skills/
```

---

## 📋 Cognitive Structuring Invariants

Every generated mindmap adheres strictly to official Markmap standards and information architecture principles:

* **Miller's Law (4–7 Main Branches `##`)**: Limits top-level branches to match human working memory capacity. Always cluster related concepts into umbrella categories rather than dumping flat lists.
* **MECE Taxonomy (Mutually Exclusive, Collectively Exhaustive)**: Sibling branches at the same depth share a single logical classification axis (e.g. system layers, data lifecycle stages, or user personas) without semantic overlap.
* **Branch Density Equilibrium**: Automatically partitions lop-sided branches (> 7 children) into intermediate sub-groups (`###`) to maintain visual balance.
* **Progressive Disclosure (`<!-- markmap: fold -->`)**: High-level branches (Tiers 1–2) remain open for 5-second scanning, while deep implementation nodes (depth ≥ 3) or dense technical parameters fold by default to prevent visual fatigue.
* **Decision & Status Encoding**:
  - `- [x]` Completed / Confirmed milestone
  - `- [ ]` Open Question / Pending decision
  - `~~Discarded Alternative~~`: Documents why an option was rejected
  - `==Critical Path / Bottleneck==`: Highlights focal architectural risks
  - `+ Advantage / - Cost Dyads`: Explicitly states who pays the trade-off

```markdown
---
title: Finolabs Agent Gateway Architecture
markmap:
  colorFreezeLevel: 2
---

## Ingress Gateway (MECE: Ingress)
- **Runtime**: Cloudflare Workers
- **Security**: JWT with RSA signatures
- ~~Alternative: Self-hosted Kong (High idle cost)~~

## Storage Tier (MECE: Persistence)
- **Metadata**: Cloudflare D1 (SQLite)
  - `+ Low latency, zero cold starts`
  - `- Single-writer concurrency ceiling`
- **Blobs**: Cloudflare R2 object store
- ~~Alternative: AWS S3 (High egress fees)~~

## Telemetry (MECE: Observability) <!-- markmap: fold -->
- **Traces**: OpenTelemetry collector
- **Metrics**: Cloudflare Analytics Engine
- **Pending Tasks**:
  - - [ ] Benchmark 5% trace sampling rate
  - - [x] Enable tail-based sampling
```

---

## 🔄 Opportunistic Multi-Skill Synergy

`markmap-skills` can structure a mindmap without auxiliary skills. HTML rendering has the requirements listed above. When complementary skills are already available in the host agent, their outputs can also become mindmap inputs:

| Skill in Harness | Upstream Role | `markmap` Downstream Role |
|---|---|---|
| **`grilling`** | Stress-tests ideas, exposes hidden assumptions, challenges trade-offs. | **Visual Decision Tree**: Synthesizes grilled decisions, struck-out options (`~~...~~`), and confirmed invariants. |
| **`brainstorming`** | Divergent thinking, exploratory ideation, sprawling idea generation. | **Convergent Affinity Map**: Gathers unstructured ideas into 4–7 MECE categories with actionable checkboxes. |
| **Spec Kit (`.specify/`)** | Defines formal functional specifications (`spec.md`). | **Functional Decomposition**: Visually maps user stories, data entities, and acceptance criteria. |

### Practical Synergy Scenarios:

#### Scenario 1: Paired with `grilling`
> **User Prompt:** *"Use grilling to stress-test this architecture proposal, then synthesize the decisions into a mindmap."*
> 
> **Agent Execution:**
> 1. Runs `grilling` to probe boundary conditions, unearth trade-offs, and challenge assumptions.
> 2. Finalizes core architectural agreements.
> 3. Handoff to `markmap` to emit `.mindmap.md`: highlighting confirmed paths, crossing out discarded alternatives (`~~...~~`), and flagging remaining open loops (`- [ ]`).

#### Scenario 2: Paired with `brainstorming`
> **User Prompt:** *"Brainstorm 10 growth features for this product, then organize them into a clean mindmap."*
> 
> **Agent Execution:**
> 1. Runs `brainstorming` for divergent ideation.
> 2. Invokes `markmap` to converge ideas into 4–7 MECE clusters (e.g. Acquisition, Activation, Retention, Monetization).
> 3. Applies `<!-- markmap: fold -->` to secondary branches and emits an interactive HTML artifact.

#### Scenario 3: Standalone Execution
> When auxiliary skills are absent from the harness, `markmap` processes user requests directly, **never prompting or nagging the user to install additional packages**.

---

## 🛠️ Repository Architecture

```text
markmap-skills/
├── .github/
│   ├── workflows/
│   │   └── ci.yml              # Automated GitHub Actions CI workflow
│   ├── ISSUE_TEMPLATE/         # Structured bug & feature request templates
│   └── PULL_REQUEST_TEMPLATE.md# Pull request validation checklist
├── .antigravity-plugin/
│   └── plugin.json             # Antigravity plugin manifest
├── .claude-plugin/
│   └── plugin.json             # Claude Code plugin manifest (with URLs & icons)
├── .codex-plugin/
│   └── plugin.json             # OpenAI Codex plugin manifest (interface & translations)
├── .codex/
│   └── plugin.json             # Legacy Codex compatibility manifest
├── agents/
│   └── openai.yaml             # Legacy interface descriptor; canonical copy is in the skill
├── package.json                # npm package descriptor (skills.sh discovers SKILL.md)
├── assets/
│   ├── icon.svg                # Vector SVG icon (FINOLABS Design System)
│   ├── icon-dark.svg           # Dark mode vector SVG icon
│   └── icon.png                # 512x512 PNG marketplace icon
├── logo.svg                    # Root vector logo
├── LICENSE                     # MIT License
├── README.md                   # Product documentation & usage guide
├── CONTRIBUTING.md             # Contribution guidelines & offline testing
├── PRIVACY.md                  # Privacy policy & data governance
├── TERMS.md                    # Terms of service
├── skills/
│   └── markmap/
│       ├── SKILL.md            # Canonical skill instructions & prompt constraints
│       ├── agents/openai.yaml  # Skill-local Codex UI metadata
│       ├── scripts/render.sh   # Pinned renderer, included in skill installs
│       └── assets/
│           └── template.html   # CDN template with CSP and plain-text labels
├── scripts/
│   ├── build_icon.py           # Portable vector icon renderer
│   ├── render.sh               # Hardened CLI helper (markmap-cli wrapper)
│   └── sync_version.sh         # Propagates package.json version to every manifest
└── tests/
    └── validate.sh             # Automated validation & test suite (8 gates)
```

---

## 🔒 Security Posture & Privacy

* **No Maintainer Backend or Telemetry**: Host agent data policies apply. CDN HTML requests pinned libraries from jsDelivr; first CLI rendering may download packages from npm. Compiled `--offline` output embeds libraries. Skills CLI installation has its own optional telemetry.
* **Template Content Isolation**: JSON-encode Markdown and escape every `<` before embedding; HTML-escape titles. CDN template nodes display source text with links, images, and raw HTML disabled. The CSP is defense in depth, not a substitute for encoding. CLI-generated HTML has its own rendering behavior; use trusted source content.
* **CLI Option Injection Guard**: `scripts/render.sh` terminates argument parsing with `--` (`markmap-cli@0.18.12 --offline -o "$OUTPUT" --no-open -- "$INPUT"`) to prevent untrusted input from triggering CLI flags.
* **Sensitive Data Policy**: See [PRIVACY.md](PRIVACY.md) and [TERMS.md](TERMS.md).

---

## 📄 License & Community

* **License**: [MIT License](LICENSE) © [Fioenix](https://github.com/fioenix)
* **Contributing**: Read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting pull requests.
* **Issues & Feedback**: [GitHub Issues](https://github.com/finolabs/markmap-skills/issues)
