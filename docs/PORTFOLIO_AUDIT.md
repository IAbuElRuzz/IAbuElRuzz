# Portfolio audit and implementation roadmap

Audit date: 7 November 2026. Scope: public GitHub repositories owned by IAbuElRuzz; source snapshots inspected without changing project repositories.

## Portfolio findings

The original README contained only a greeting and WakaTime statistics. It did not identify the engineer, explain a project, show architecture, or provide a collaboration route. The historical statistics and update markers are preserved inside a disclosure so the existing workflow can continue updating them.

The paginated GitHub API returned 201 public repositories: 20 marked non-fork and 181 forks. StoryOS was fetched separately after being requested; it was absent from that earlier enumeration. Metadata was reviewed for every enumerated repository. Source snapshots were downloaded for all 20 non-fork entries and StoryOS; detailed implementation review focused on the five featured projects and stronger supporting candidates. Forks were not exhaustively reviewed or attributed as original accomplishments. GitHub's non-fork flag also does not establish authorship: the Angular dropdown package explicitly credits upstream work.

The public profile has no website, public email, or Twitter account configured. Its bio is an unreadable encoded string. Only GitHub is used for contact; no LinkedIn identity was inferred. Replace the public name with Ibrahim Abu El Ruzz and the bio with a concise AI/security engineering statement through profile settings.

The redesign puts professional identity and source-backed projects first. A single-column project layout avoids wide project cards on mobile. One local static image avoids external badge failures; text provides the same essential information. No hiring, adoption, benchmark, employment, or production deployment claims were inferred from source code.

## Technical comparison

| Project | Problem and contribution | Verified implementation | Boundaries |
| --- | --- | --- | --- |
| [RepoSpect](https://github.com/IAbuElRuzz/RepoSpect) | Inspect potentially dangerous repository behavior before execution | Go CLI; acquisition, scanner, revision, dependencies, reporting packages; lexical rules, manifest parsers, literal reference graph; lifecycle/credential/network correlation; optional exact-version OSV lookup; multiple report formats; coverage and redaction controls | Early development. References are not calls or dataflow. Initial Dockerfile/config rules are not OCI image scanning. Dependency confusion, provenance verification, and general exfiltration/dataflow analysis must not be presented as solved. |
| [RepoSentry](https://github.com/IAbuElRuzz/RepoSentry) | Lightweight local security triage | Python standard-library runtime; argparse CLI; scanner/rules/models/render modules; source patterns, lifecycle hooks, workflow risks, dependency URL checks; optional PyPI/npm metadata; Markdown and JSON | Alpha 0.1. No cross-file attack graph, lockfile resolution, OSV or SARIF implementation. Registry checks concern latest metadata rather than the exact installed dependency version. Per-file size filtering does not establish a global scan budget. Raw evidence can include source text; redact before sharing reports. |
| [RepoSignal](https://github.com/IAbuElRuzz/RepoSignal) | Give maintainers actionable repository presentation and maintenance feedback | Dependency-free REST client, audit rules, typed report models, Markdown renderer and CLI; description/topics, root community files, selected runtime artifacts | Version 0.1. Root listing and metadata, not recursive source security analysis. Does not inspect actual workflow health or dependency vulnerabilities. No identity, trustworthiness, or hiring verdicts. |
| [PDF-Rag](https://github.com/IAbuElRuzz/PDF-Rag) | Query local PDFs through retrieval rather than placing entire documents in a prompt | PyPDF2/pdfplumber extraction; 1,000-character chunks with 200 overlap; MiniLM embeddings; FAISS persistence; LangChain RetrievalQA; Ollama llama3; retrieved-context display in alternative script | Prototype. No retrieval evaluation, citation UI, OCR, service API or production readiness established. Local model use does not guarantee offline installation; embeddings may need downloading. |
| [StoryOS](https://github.com/IAbuElRuzz/StoryOS) | Apply incremental build concepts to video generation | YAML parser/compiler; video/voice/merge/concat nodes; SHA-256-derived keys from params and upstream hashes; four-worker independent-node execution; sequential dependent nodes; JSON cache manifest; Runway SDK adapter; FFmpeg processing | v0.1 prototype. ElevenLabs adapter emits a tone. API exceptions fall back to mock output. Cache keys do not guarantee deterministic generated media, adapter-version invalidation or production-safe caching. No live API success claimed. |

RepoSpect and RepoSentry overlap in static review, but have separate languages, architecture and scope. There is no evidence here that either replaces the other. RepoSignal examines repository maintenance metadata, not malicious code. PDF-Rag demonstrates retrieval integration; StoryOS demonstrates workflow compilation and asset orchestration.

## Engineering evidence and documentation readiness

| Repository | Tests and automation | Releases/license | Community documentation |
| --- | --- | --- | --- |
| RepoSpect | Go tests; CI matrix for Linux/macOS/Windows with race tests, vet and build; latest observed CI failed | No releases observed; Apache-2.0; release workflow present | Architecture, threat model, limits, hardening, status, roadmap, SECURITY, CONTRIBUTING, issue and PR templates |
| RepoSentry | pytest source; release-triggered test/build/publish workflow succeeded; no push/PR test workflow found | One release observed; MIT | Installation and examples present; no separate architecture, SECURITY, CONTRIBUTING or issue templates found |
| RepoSignal | pytest source; no workflow runs or CI workflow found | No releases observed; MIT | Quick start and roadmap; no separate architecture, SECURITY, CONTRIBUTING or issue templates found |
| PDF-Rag | No test suite or CI found | No releases observed; README says MIT but no LICENSE file found | Duplicate features, placeholder clone URL, nonexistent main.py, missing pdfplumber dependency |
| StoryOS | Strict mypy configuration exists; no test suite or CI found | No root LICENSE found; releases not queried | YAML examples and architecture sketch; no SECURITY, CONTRIBUTING or issue templates found |

A workflow definition is not proof of a passing run. Latest RepoSpect run: [failed CI at the audited revision](https://github.com/IAbuElRuzz/RepoSpect/actions/runs/42379716639). Local Go tests passed during this audit; the remote failure remains unresolved.

## Prioritized repository roadmap

These are recommendations only. No flagship repository was modified.

1. **P0 — Correct reproducibility and trust gaps.** Investigate RepoSpect's failed remote matrix before advertising passing CI. Fix PDF-Rag's clone URL, duplicated sections and main.py/run.py mismatch; add pdfplumber and pin a compatible dependency set. Document trusted-only pickle/FAISS cache loading, remove generated indexes from source as appropriate, and provide safe cache invalidation. Add an explicit LICENSE after owner choice rather than relying on the README's MIT sentence. In StoryOS, distinguish mock and API results in manifests, support explicit failure instead of silent fallback, validate identifiers/paths and empty graphs, and include adapter/model versions and mode in cache keys.
2. **P1 — Establish repeatable checks.** Add push/PR CI for RepoSentry and RepoSignal; run tests, build artifacts and verify installation from a clean environment. Add PDF ingestion/retrieval smoke tests with synthetic public fixtures and no model-service dependency. Test StoryOS hash invalidation, dependency order, failed renders, and mock output. Pin third-party Actions by full SHA, use least privilege, and add dependency update automation.
3. **P1 — Make evidence easy to inspect.** Record RepoSpect's inert fixture scan and trace in a short terminal GIF with version and command visible. For RepoSentry show a synthetic local scan and JSON report with redacted evidence. For RepoSignal audit a controlled fixture or clearly dated public repository; show evidence-linked recommendations. For PDF-Rag show a public sample PDF, retrieved passages and answer with measured retrieval checks. For StoryOS record cold render, cached rerun and one changed-shot rebuild; visibly label mock output. No GIF or live model demo was fabricated in this task.
4. **P2 — Document architecture and limitations.** Add small Mermaid diagrams to RepoSentry (walk → rules/metadata → report), RepoSignal (REST → audit → evidence report), PDF-Rag (extract → chunk → embed → FAISS → retrieval → Ollama), and StoryOS (YAML → nodes → cache/executor → FFmpeg). Document install prerequisites, failure modes and test commands. RepoSpect already has substantial architecture and threat-model documentation.
5. **P2 — Open-source readiness.** Add missing SECURITY.md, CONTRIBUTING.md, issue/PR templates and maintainer support expectations. Publish source-build or package installation instructions validated against actual releases. Separate shipped functionality from planned features. Add changelogs and versioned release notes; verify distributable licensing and generated asset provenance.
6. **P3 — Measure quality before expanding scope.** Use labeled benign/security fixtures and report precision/false positives for scanners; retrieval relevance and grounded answers for PDF-Rag; invalidation correctness and explicit cold/warm timing methodology for StoryOS. Publish results only after measurement. Extend tracing, dependency resolution and AI features behind documented boundaries.

## Discoverability and profile checklist

All four original flagships had empty topics at enumeration; StoryOS also had no topics and no description. The three security/intelligence descriptions were already materially accurate. Suggested settings below require separate authorization to apply.

| Project | Suggested description | Focused topics |
| --- | --- | --- |
| RepoSpect | Local-first Go CLI for static repository security analysis, installation-script review, and inferred execution-path tracing. | golang, cli, static-analysis, repository-security, supply-chain-security, sarif |
| RepoSentry | Python CLI for local repository security triage and optional PyPI/npm dependency metadata checks. | python, cli, static-analysis, dependency-analysis, github-actions, security-tools |
| RepoSignal | Evidence-based CLI audits for public GitHub repository documentation, discoverability, and maintenance signals. | python, github-api, cli, repository-audit, developer-tools, documentation |
| PDF-Rag | Local PDF question answering with MiniLM embeddings, FAISS retrieval, LangChain, and Ollama. | python, rag, pdf, faiss, ollama, semantic-search |
| StoryOS | YAML-driven video pipeline with content-addressed asset caching, parallel generation, and FFmpeg assembly. | python, video-generation, workflow-engine, ffmpeg, build-system, generative-ai |

Recommended six pins, in order:

1. **RepoSpect:** strongest security architecture, documented safety boundary and visual workflow.
2. **RepoSentry:** approachable Python security tool, tests and an observed release workflow.
3. **RepoSignal:** a distinct maintainer-facing product with separable acquisition, rules and reporting.
4. **PDF-Rag:** practical retrieval/LLM integration; prioritize documentation fixes before promotion.
5. **StoryOS:** incremental builds and dependency-aware media workflows broaden the systems story.
6. **llm-orca:** TypeScript CLI provider adapters, project profiles, bounded context packing, parallel provider comparison and transcript storage. Its comparison scoring is heuristic and its sandbox modes are wrapper hints, not independently enforced security boundaries.

Supporting candidates: crypto-ai-agent confirms FastAPI, SQLAlchemy and tool-using LangChain integration, but requires dependency/API hardening and does not validate financial predictions. AES_Tiny provides an OpenSSL C wrapper and Python ctypes examples, but is not evidence of audited cryptography. Angular dropdown repositories demonstrate component work, with upstream attribution and older dependencies to clarify. AgentSkills/CodingAgents are instruction/configuration collections, not autonomous runtime implementations. Older UI experiments and generic template READMEs are weaker pin candidates. Forks are not credited as upstream contributions without commit/PR evidence.

Profile settings: use the verified full name, replace the encoded bio, apply the six pins, and add professional links only after identity verification. Do not use follower or contribution counts as evidence of engineering quality. No externally merged contributions or maintainer support commitments were established by this audit.

## Extended portfolio recommendation

GitHub Pages would help once reproducible demos and case studies exist. It is lower priority than correcting setup and CI gaps. No website was built.

1. Prepare three case studies: RepoSpect's safety model and tracing limits, PDF-Rag's retrieval decisions and evaluation, StoryOS's cache invalidation and scheduling tradeoffs.
2. Add genuine screenshots, accessible transcripts, small architecture diagrams, and versioned source links. Use public synthetic fixtures and distinguish mock from live results.
3. Build a small static Pages site with dedicated project pages, evidence links, mobile layouts and native theme support. Keep the README as the fast entry point.
4. Add a tested deployment workflow after explicit publication authorization. Validate links and accessibility; prefer static demos until hosting and API costs justify interactive services.
