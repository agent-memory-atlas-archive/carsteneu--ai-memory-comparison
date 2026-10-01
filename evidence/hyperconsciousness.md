# Hyperconsciousness evidence

Maintainer submission from Louis Beaumont, prepared with Codex assistance. Reviewed on 2026-10-01 against public commit `d619a4e59be9c33121389b9cf14e5a93b47b3eb4`. This audit covers the public engine and its documented integrations. Private Companion and private agent orchestration are excluded. A ❌ means the feature is not established under this template's definition in the checked public revision.

**Repo:** `github.com/louis030195/hyperconsciousness`  
**Stars:** 2 (2026-10-01 GitHub API snapshot)  
**Language:** Rust  
**License:** MIT ([LICENSE](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/LICENSE#L1))  
**Created:** 2026-09-14  
**Description:** Developer-alpha encrypted, append-only knowledge store with a Rust CLI, MCP/HTTP access, device sync and scoped expiring grants.

## System Metadata

| Field | Value |
|-------|-------|
| **Deployment** | Local CLI / self-hosted MCP or HTTP |
| **Storage** | Signed append-only logs, encrypted blobs and rebuildable encrypted indexes |
| **Integration** | CLI / MCP / HTTP / instruction skills |
| **Single binary?** | Yes for the engine/CLI; optional dashboard is separate |
| **Setup** | Build from source with Rust 1.88: `cargo build --release --locked` |
| **Pricing** | Free (MIT) |
| **Storage unit** | Signed encrypted record with JSON payload; file blobs stored separately |

Metadata sources: [README](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/README.md#L5), [source installation](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/README.md#L102), [record format](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/record.rs#L5), and [storage architecture](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/ARCHITECTURE.md#L48).

## Architecture

### Proxy ❌

### Web/TUI ✅

- Source: [README.md#L73](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/README.md#L73). Optional HC Atlas browser dashboard in this repository. It is installed separately from the CLI and can search records with an authenticated reader; it does not provide hosted team access.

### Offline ✅

- Source: [README.md#L130](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/README.md#L130). Local store creation, writing and reading use an explicit directory.
- Source: [docs/RANKED_RECALL.md#L46](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/RANKED_RECALL.md#L46). Retrieval runs on the authorized node with no model or embedding service.

### Multi-agent ✅

- Source: [docs/COMPANY-ACCESS.md#L12](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/COMPANY-ACCESS.md#L12). Multiple human/agent principals can access shared records through separate scoped grants and member/group policy. This is shared memory access, not agent orchestration.

### LLM providers (count: 0) ❌

- Source: [docs/RANKED_RECALL.md#L46](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/RANKED_RECALL.md#L46). Zero built-in LLM/embedding providers. Clients may use their own models; those are outside the engine.

### Cache optimization ✅

- Source: [src/mcp.rs#L241](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L241). The MCP server retains a snapshot only while signed log heads and the runtime-key fingerprint match.
- Source: [docs/ARCHITECTURE.md#L48](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/ARCHITECTURE.md#L48). Bounded process-local snapshots and rebuildable encrypted search indexes accelerate repeated reads.

### Procedural memory ❌

Captured procedure candidates remain evidence; retrieval does not execute them.

### Sandboxed execution ❌

No code sandbox. Grants do not isolate a process with access to owner files or keys.

### Scheduled/autonomous ✅

- Source: [skills/hyperconsciousness-ops/SKILL.md#L309](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/skills/hyperconsciousness-ops/SKILL.md#L309). An explicitly installed store-scoped scheduler runs outbound encrypted sync through launchd, systemd or Windows Task Scheduler. This covers replication only; it does not schedule agent reasoning or business workflows.

### Privacy/encrypt ✅

- Source: [src/record.rs#L133](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/record.rs#L133). Payloads are sealed and records signed before storage.
- Source: [README.md#L193](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/README.md#L193). Grants constrain server responses. Owner OS/key access remains outside that boundary, and hosted model providers see returned plaintext. Developer alpha; no independent security audit claimed.

### Data export ✅

- Source: [src/main.rs#L5871](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/main.rs#L5871). The built-in hc bundle command exports signed history and encrypted chunks to a portable file, consumed by hc import. This is a ciphertext archive, not a Markdown/JSON memory export.

## Data Model

### Entities ❌

### Actions ❌

### Keywords/tags ✅

- Source: [src/mcp.rs#L2183](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L2183). Writes accept a kind and explicit string tags; labels are validated before append.

### Anticipated queries ❌

### Trigger rules ❌

### Domain tag ❌

### Task type ❌

### Context (why) ❌

### Source attribution ❌

Capture producer/material/source refs are stored, but producer claims are explicitly unverified. The four material categories do not establish the required three explicit author categories.

### Origin + trust ❌

### Emotional ❌

### Conflict surfacing ❌

Same-source/version conflicts are suppressed and rejected on retry. No semantic conflict review surface is claimed.

### Layered memory ❌

### Time-travel ✅

- Source: [src/mcp.rs#L2461](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L2461). The recent tool supports since/until temporal filtering and chronological pagination over currently visible records. This satisfies temporal search; superseded/retracted text is hidden from normal reads, so arbitrary historical as-of-state queries are not claimed.

### Schema fields (count: 6) ✅

- Source: [src/mcp.rs#L2153](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L2153). Six caller-supplied top-level fields in RememberInput: text, kind, tags, sensitivity, context and change. Optional context/change count once each; nested fields and generated grant/provenance/identity/timestamp fields are excluded.

## Search & Retrieval

### Full-text ✅

- Source: [docs/RANKED_RECALL.md#L22](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/RANKED_RECALL.md#L22). Literal substring search is the default; opt-in lexical relevance uses Unicode word tokenization, prefix matching and BM25. No embeddings.

### Semantic/vector ❌

### Hybrid (BM25+Vec) ❌

### Deep (incl. thinking) ❌

### Code graph ❌

### Docs search ❌

### Fact metadata query ✅

- Source: [src/mcp.rs#L2443](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L2443). Search can filter by kind, tags, since and until inside the current grant. There is no arbitrary SQL/query language or built-in unfinished-task ontology.

### Timeline view ✅

- Source: [src/mcp.rs#L2461](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L2461). Chronological recent records with since/until date bounds and continuation cursors.

### Search modes (count: 3) ✅

- Source: [src/mcp.rs#L2430](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L2430). Three text retrieval modes counted: search literal, search relevance and recent chronological browsing. Point-record expansion and file listing are excluded from this count.

### Data sources (count: 1) ✅

- Source: [src/mcp.rs#L2430](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/src/mcp.rs#L2430). Conservative count: stored record text. Imported chats/documents/handoffs can supply that text, but instruction-only ingestion recipes are not counted as separate native searchable connectors.

## Knowledge Lifecycle

### Decay/forgetting ❌

### Supersede/replace ✅

- Source: [docs/CAPTURE-CONTEXT.md#L80](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/CAPTURE-CONTEXT.md#L80). Versioned source captures support higher-version upserts. The logical source is bound to the authenticated principal and declared source identity; readers suppress superseded versions while signed history is retained.

### Contradiction detection ❌

No automatic semantic contradiction detection. Same-version payload conflict handling is an integrity rule.

### Quarantine ❌

### Auto-resolution ❌

### Trust model ❌

### Explicit forget ✅

- Source: [docs/CAPTURE-CONTEXT.md#L99](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/CAPTURE-CONTEXT.md#L99). An explicit higher-version retract hides a managed text note from current retrieval. This is logical forgetting only: historical ciphertext, legacy notes and already copied plaintext are not erased (lines 136-147).

## Extraction Pipeline

### Auto-extraction ❌

The repository ships ingestion instructions; running them requires an external harness and authorized writer.

### Content-aware preprocessing ❌

### Deduplication ✅

- Source: [docs/CAPTURE-CONTEXT.md#L99](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/CAPTURE-CONTEXT.md#L99). Exact retries of a versioned capture reuse the existing record receipt. Identical same-version events converge to one search result after sync (lines 127-134). Ordinary writes remain append-only; semantic/near-duplicate merging is not provided.

### Quality refinement ❌

### Narrative generation ❌

External harnesses may write task handoffs. The engine does not generate summaries.

### Clustering ❌

### Recurrence detection ❌

### Persona extraction ❌

## Platform Support

### Claude Code ✅

- Source: [README.md#L59](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/README.md#L59). The shipped ingestion instruction skills document installation into ~/.claude/skills. Existing authorized source access and an HC writer are prerequisites; installation does not connect accounts or run ingestion.

### Codex ✅

- Source: [docs/HOSTED-ACCESS.md#L7](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/HOSTED-ACCESS.md#L7). hc setup with --codex registers the native executable as a named Codex MCP server and installs supplied instruction-only skills. Local MCP configuration is also documented in README lines 149-186.

### OpenCode ❌

### Gemini CLI ❌

### Copilot ❌

### Cursor ❌

### Windsurf ❌

### OpenClaw ❌

### Hermes ❌

A generic skill mentions Hermes, but its referenced installation helper is absent in the checked public revision. A working dedicated integration is not established here.

### pi/omp ❌

A generic skill mentions Pi, but its referenced installation helper is absent in the checked public revision. A working dedicated integration is not established here.

### Antigravity ❌

## Benchmarks

### LoCoMo ❌

### LongMemEval ❌

### PersonaMem ❌

### Token reduction ❌

### Methodology open ✅

- Source: [docs/SCALABILITY-BENCHMARK.md#L73](https://github.com/louis030195/hyperconsciousness/blob/d619a4e59be9c33121389b9cf14e5a93b47b3eb4/docs/SCALABILITY-BENCHMARK.md#L73). Public synthetic storage/retrieval benchmark methodology states hardware, baseline, samples, limits and reproduction commands using examples/run_dimensions.py. This is not a LoCoMo, LongMemEval, PersonaMem or model-answer benchmark.

