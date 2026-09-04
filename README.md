<p align="center">
  <img src="assets/banner.png" alt="Hermes Agent" width="100%">
</p>

# Hermes Agent ☤
<p align="center">
  <a href="https://hermes-agent.nousresearch.com/">Hermes Agent</a> | <a href="https://hermes-agent.nousresearch.com/">Hermes Desktop</a>
</p>
<p align="center">
  <a href="https://hermes-agent.nousresearch.com/docs/"><img src="https://img.shields.io/badge/Docs-hermes--agent.nousresearch.com-FFD700?style=for-the-badge" alt="Documentation"></a>
  <a href="https://discord.gg/NousResearch"><img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/NousResearch/hermes-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License: MIT"></a>
  <a href="https://nousresearch.com"><img src="https://img.shields.io/badge/Built%20by-Nous%20Research-blueviolet?style=for-the-badge" alt="Built by Nous Research"></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/Lang-中文-red?style=for-the-badge" alt="中文"></a>
  <a href="README.ur-pk.md"><img src="https://img.shields.io/badge/Lang-اردو-green?style=for-the-badge" alt="اردو"></a>
  <a href="README.es.md"><img src="https://img.shields.io/badge/Lang-Español-orange?style=for-the-badge" alt="Español"></a>
</p>

**The self-improving AI agent built by [Nous Research](https://nousresearch.com).** It's the only agent with a built-in learning loop — it creates skills from experience, improves them during use, nudges itself to persist knowledge, searches its own past conversations, and builds a deepening model of who you are across sessions. Run it on a $5 VPS, a GPU cluster, or serverless infrastructure that costs nearly nothing when idle. It's not tied to your laptop — talk to it from Telegram while it works on a cloud VM.

Use any model you want — [Nous Portal](https://portal.nousresearch.com), OpenRouter, OpenAI, your own endpoint, and [many others](https://hermes-agent.nousresearch.com/docs/integrations/providers). Switch with `hermes model` — no code changes, no lock-in.

<table>
<tr><td><b>A real terminal interface</b></td><td>Full TUI with multiline editing, slash-command autocomplete, conversation history, interrupt-and-redirect, and streaming tool output.</td></tr>
<tr><td><b>Lives where you do</b></td><td>Telegram, Discord, Slack, WhatsApp, Signal, and CLI — all from a single gateway process. Voice memo transcription, cross-platform conversation continuity.</td></tr>
<tr><td><b>A closed learning loop</b></td><td>Agent-curated memory with periodic nudges. Autonomous skill creation after complex tasks. Skills self-improve during use. FTS5 session search with LLM summarization for cross-session recall. <a href="https://github.com/plastic-labs/honcho">Honcho</a> dialectic user modeling. Compatible with the <a href="https://agentskills.io">agentskills.io</a> open standard.</td></tr>
<tr><td><b>Scheduled automations</b></td><td>Built-in cron scheduler with delivery to any platform. Daily reports, nightly backups, weekly audits — all in natural language, running unattended.</td></tr>
<tr><td><b>Delegates and parallelizes</b></td><td>Spawn isolated subagents for parallel workstreams. Write Python scripts that call tools via RPC, collapsing multi-step pipelines into zero-context-cost turns.</td></tr>
<tr><td><b>Runs anywhere, not just your laptop</b></td><td>Seven terminal backends — local, Docker, SSH, Singularity, Modal, Daytona, and Vercel Sandbox. Daytona and Modal offer serverless persistence — your agent's environment hibernates when idle and wakes on demand, costing nearly nothing between sessions. Run it on a $5 VPS or a GPU cluster.</td></tr>
<tr><td><b>Research-ready</b></td><td>Batch trajectory generation, trajectory compression for training the next generation of tool-calling models.</td></tr>
</table>

---

## Quick Install

### Linux, macOS, WSL2, Termux

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

### Windows (native, PowerShell)

> **Heads up:** Native Windows runs Hermes without WSL — CLI, gateway, TUI, and tools all work natively. If you'd rather use WSL2, the Linux/macOS one-liner above works there too. Found a bug? Please [file issues](https://github.com/NousResearch/hermes-agent/issues).

Run this in PowerShell:

```powershell
iex (irm https://hermes-agent.nousresearch.com/install.ps1)
```

The installer handles everything: uv, Python 3.11, Node.js, ripgrep, ffmpeg, **and a portable Git Bash** (MinGit, unpacked to `%LOCALAPPDATA%\hermes\git` — no admin required, completely isolated from any system Git install). Hermes uses this bundled Git Bash to run shell commands.

If you already have Git installed, the installer detects it and uses that instead. Otherwise a ~45MB MinGit download is all you need — it won't touch or interfere with any system Git.

> **Android / Termux:** The tested manual path is documented in the [Termux guide](https://hermes-agent.nousresearch.com/docs/getting-started/termux). On Termux, Hermes installs a curated `.[termux]` extra because the full `.[all]` extra currently pulls Android-incompatible voice dependencies.
>
> **Windows:** Native Windows is fully supported — the PowerShell one-liner above installs everything. If you'd rather use WSL2, the Linux command works there too. Native Windows install lives under `%LOCALAPPDATA%\hermes`; WSL2 installs under `~/.hermes` as on Linux.

After installation:

```bash
source ~/.bashrc    # reload shell (or: source ~/.zshrc)
hermes              # start chatting!
```

### Troubleshooting

#### Windows Defender or antivirus flags `uv.exe` as malware

If your antivirus (Bitdefender, Windows Defender, etc.) quarantines `uv.exe` from the Hermes `bin` folder (`%LOCALAPPDATA%\hermes\bin\uv.exe`), this is a **false positive**. The file is Astral's `uv` — the Rust Python package manager Hermes bundles to manage its Python environment. ML-based antivirus engines commonly flag unsigned Rust binaries that download and install packages.

**To verify your copy is authentic:**

```powershell
# Install GitHub CLI if needed
winget install --id GitHub.cli

# Login to GitHub
gh auth login

# Run verification
$uv = "$env:LOCALAPPDATA\hermes\bin\uv.exe"
$ver = (& $uv --version).Split(' ')[1]
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$zip = "$env:TEMP\uv.zip"
Invoke-WebRequest "https://github.com/astral-sh/uv/releases/download/$ver/uv-x86_64-pc-windows-msvc.zip" -OutFile $zip -UseBasicParsing
gh attestation verify $zip --repo astral-sh/uv
Expand-Archive $zip "$env:TEMP\uv_x" -Force
(Get-FileHash "$env:TEMP\uv_x\uv.exe").Hash -eq (Get-FileHash $uv).Hash
```

If attestation says "Verification succeeded" and the last line prints `True`, you're good.

**To whitelist Hermes:**
- **Windows Defender:** Run PowerShell as Admin → `Add-MpPreference -ExclusionPath "$env:LOCALAPPDATA\hermes\bin"`
- **Bitdefender:** Add an exception in the Bitdefender console (Protection > Antivirus > Settings > Manage Exceptions)
- Whitelist the **folder**, not the file hash — Hermes updates `uv` and the hash changes every version

For more context, see the upstream Astral reports: [astral-sh/uv#13553](https://github.com/astral-sh/uv/issues/13553), [astral-sh/uv#15011](https://github.com/astral-sh/uv/issues/15011), [astral-sh/uv#10079](https://github.com/astral-sh/uv/issues/10079).

---

## Getting Started

```bash
hermes              # Interactive CLI — start a conversation
hermes model        # Choose your LLM provider and model
hermes tools        # Configure which tools are enabled
hermes config set   # Set individual config values
hermes config get   # Print individual config values
hermes gateway      # Start the messaging gateway (Telegram, Discord, etc.)
hermes setup        # Run the full setup wizard (configures everything at once)
hermes claw migrate # Migrate from OpenClaw (if coming from OpenClaw)
hermes update       # Update to the latest version
hermes doctor       # Diagnose any issues
```

📖 **[Full documentation →](https://hermes-agent.nousresearch.com/docs/)**

---

## Skip the API-key collection — Nous Portal

Hermes works with whatever provider you want — that's not changing. But if you'd rather not collect five separate API keys for the model, web search, image generation, TTS, and a cloud browser, **[Nous Portal](https://portal.nousresearch.com)** covers all of them under one subscription:

- **300+ models** — pick any of them with `/model <name>`
- **Tool Gateway** — web search (Firecrawl), image generation (FAL), text-to-speech (OpenAI), cloud browser (Browser Use), all routed through your sub. No extra accounts.

One command from a fresh install:

```bash
hermes setup --portal
```

That logs you in via OAuth, sets Nous as your provider, and turns on the Tool Gateway. Check what's wired up any time with `hermes portal info`. Full details on the [Tool Gateway docs page](https://hermes-agent.nousresearch.com/docs/user-guide/features/tool-gateway).

You can still bring your own keys per-tool whenever you want — the gateway is per-backend, not all-or-nothing.

---

## CLI vs Messaging Quick Reference

Hermes has two entry points: start the terminal UI with `hermes`, or run the gateway and talk to it from Telegram, Discord, Slack, WhatsApp, Signal, or Email. Once you're in a conversation, many slash commands are shared across both interfaces.

| Action                         | CLI                                           | Messaging platforms                                                              |
| ------------------------------ | --------------------------------------------- | -------------------------------------------------------------------------------- |
| Start chatting                 | `hermes`                                      | Run `hermes gateway setup` + `hermes gateway start`, then send the bot a message |
| Start fresh conversation       | `/new` or `/reset`                            | `/new` or `/reset`                                                               |
| Change model                   | `/model [provider:model]`                     | `/model [provider:model]`                                                        |
| Set a personality              | `/personality [name]`                         | `/personality [name]`                                                            |
| Retry or undo the last turn    | `/retry`, `/undo`                             | `/retry`, `/undo`                                                                |
| Compress context / check usage | `/compress`, `/usage`, `/insights [--days N]` | `/compress`, `/usage`, `/insights [days]`                                        |
| Browse skills                  | `/skills` or `/<skill-name>`                  | `/<skill-name>`                                                                  |
| Interrupt current work         | `Ctrl+C` or send a new message                | `/stop` or send a new message                                                    |
| Platform-specific status       | `/platforms`                                  | `/status`, `/sethome`                                                            |

For the full command lists, see the [CLI guide](https://hermes-agent.nousresearch.com/docs/user-guide/cli) and the [Messaging Gateway guide](https://hermes-agent.nousresearch.com/docs/user-guide/messaging).

---

## Documentation

All documentation lives at **[hermes-agent.nousresearch.com/docs](https://hermes-agent.nousresearch.com/docs/)**:

| Section                                                                                             | What's Covered                                             |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- |
| [Quickstart](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart)                 | Install → setup → first conversation in 2 minutes          |
| [CLI Usage](https://hermes-agent.nousresearch.com/docs/user-guide/cli)                              | Commands, keybindings, personalities, sessions             |
| [Configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration)                | Config file, providers, models, all options                |
| [Messaging Gateway](https://hermes-agent.nousresearch.com/docs/user-guide/messaging)                | Telegram, Discord, Slack, WhatsApp, Signal, Home Assistant |
| [Security](https://hermes-agent.nousresearch.com/docs/user-guide/security)                          | Command approval, DM pairing, container isolation          |
| [Tools & Toolsets](https://hermes-agent.nousresearch.com/docs/user-guide/features/tools)            | 40+ tools, toolset system, terminal backends               |
| [Skills System](https://hermes-agent.nousresearch.com/docs/user-guide/features/skills)              | Procedural memory, Skills Hub, creating skills             |
| [Memory](https://hermes-agent.nousresearch.com/docs/user-guide/features/memory)                     | Persistent memory, user profiles, best practices           |
| [MCP Integration](https://hermes-agent.nousresearch.com/docs/user-guide/features/mcp)               | Connect any MCP server for extended capabilities           |
| [Cron Scheduling](https://hermes-agent.nousresearch.com/docs/user-guide/features/cron)              | Scheduled tasks with platform delivery                     |
| [Context Files](https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files)       | Project context that shapes every conversation             |
| [Architecture](https://hermes-agent.nousresearch.com/docs/developer-guide/architecture)             | Project structure, agent loop, key classes                 |
| [Contributing](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing)             | Development setup, PR process, code style                  |
| [CLI Reference](https://hermes-agent.nousresearch.com/docs/reference/cli-commands)                  | All commands and flags                                     |
| [Environment Variables](https://hermes-agent.nousresearch.com/docs/reference/environment-variables) | Complete env var reference                                 |

---

## Bundled Skills

Hermes ships with **195 skills** out of the box — modular capabilities the agent can load on demand, compatible with the [agentskills.io](https://agentskills.io) open standard. **58** are core skills (in `skills/`) and **137** are optional add-ons (in `optional-skills/`).

### Core skills (58)

<details>
<summary><b>apple</b> (4)</summary>

- **apple-notes** — Manage Apple Notes via memo CLI: create, search, edit.
- **apple-reminders** — Apple Reminders via remindctl: add, list, complete.
- **findmy** — Track Apple devices/AirTags via FindMy.app on macOS.
- **imessage** — Send and receive iMessages/SMS via the imsg CLI on macOS.

</details>

<details>
<summary><b>autonomous-ai-agents</b> (5)</summary>

- **claude-code** — Delegate coding to Claude Code CLI (features, PRs).
- **codex** — Delegate coding to OpenAI Codex CLI (features, PRs).
- **computer-use** — Drive the desktop background-first; escalate on signal.
- **hermes-agent** — Use, configure, theme, extend, and orchestrate Hermes Agent.
- **opencode** — Delegate coding to OpenCode CLI (features, PR review).

</details>

<details>
<summary><b>creative</b> (10)</summary>

- **architecture-diagram** — Dark-themed SVG architecture/cloud/infra diagrams as HTML.
- **ascii-video** — ASCII video: convert video/audio to colored ASCII MP4/GIF.
- **baoyu-infographic** — Infographics: 21 layouts x 21 styles (信息图, 可视化).
- **claude-design** — Design one-off HTML artifacts (landing, deck, prototype).
- **design-md** — Author/validate/export Google's DESIGN.md token spec files.
- **humanizer** — Humanize text: strip AI-isms and add real voice.
- **manim-video** — Manim CE animations: 3Blue1Brown math/algo videos.
- **p5js** — p5.js sketches: gen art, shaders, interactive, 3D.
- **popular-web-designs** — 54 real design systems (Stripe, Linear, Vercel) as HTML/CSS.
- **songwriting-and-ai-music** — Songwriting craft and Suno AI music prompts.

</details>

<details>
<summary><b>devops</b> (1)</summary>

- **sdlc-review** — Review Kanban handoffs and route verified outcomes.

</details>

<details>
<summary><b>email</b> (2)</summary>

- **email-inbox-triage** — Triage an inbox: prioritize threads, draft replies safely.
- **himalaya** — Himalaya CLI: IMAP/SMTP email from terminal.

</details>

<details>
<summary><b>media</b> (3)</summary>

- **gif-search** — Search/download GIFs from Tenor via curl + jq.
- **songsee** — Audio spectrograms/features (mel, chroma, MFCC) via CLI.
- **youtube-content** — YouTube transcripts to summaries, threads, blogs.

</details>

<details>
<summary><b>note-taking</b> (1)</summary>

- **obsidian** — Read, search, create, and edit notes in the Obsidian vault.

</details>

<details>
<summary><b>productivity</b> (14)</summary>

- **airtable** — Airtable REST API via curl. Records CRUD, filters, upserts.
- **box** — Box manages cloud files, sharing, search, and metadata.
- **document-to-action-items** — Extract cited obligations, deadlines, tasks from documents.
- **docx** — Create, read, edit, template, and review Word .docx files.
- **google-workspace** — Gmail, Calendar, Drive, Docs, Sheets via gws CLI or Python.
- **maps** — Geocode, POIs, routes, timezones via OpenStreetMap/OSRM.
- **meeting-action-items** — Turn meeting notes into cited decisions, owners, tickets.
- **notion** — Notion API + ntn CLI: pages, databases, markdown, Workers.
- **pdf** — PDF files: create, read, merge, fill, OCR, edit text.
- **powerpoint** — Create, read, edit .pptx decks with python-pptx.
- **product-price-monitor** — Watch product, flight, or listing prices; alert on target.
- **teams-meeting-pipeline** — Teams meeting summaries, job replay, Graph subscriptions.
- **weekly-review-planning** — Weekly reset: commitments, stalled work, next-week plan.
- **xlsx** — Create, read, edit Excel .xlsx workbooks and CSVs.

</details>

<details>
<summary><b>research</b> (4)</summary>

- **arxiv** — Search arXiv papers by keyword, author, category, or ID.
- **competitor-news-monitor** — Watch named companies for material news; cited digests.
- **grounded-citations** — Ground answers and documents in cited, verifiable sources.
- **llm-wiki** — Karpathy's LLM Wiki: build/query interlinked markdown KB.

</details>

<details>
<summary><b>social-media</b> (1)</summary>

- **xurl** — X/Twitter via xurl CLI: raw post search, posting, DM, media.

</details>

<details>
<summary><b>software-development</b> (12)</summary>

- **codebase-inspection** — Inspect codebases w/ pygount: LOC, languages, ratios.
- **dogfood** — Exploratory QA of web apps: find bugs, evidence, reports.
- **github** — GitHub via gh CLI: PRs, issues, reviews, repos, auth.
- **hermes-agent-skill-authoring** — Author in-repo SKILL.md files: frontmatter and structure.
- **inspecting-hermes-desktop-dom** — Read the live Hermes desktop DOM/CSS over CDP.
- **node-inspect-debugger** — Debug Node.js via --inspect + Chrome DevTools Protocol CLI.
- **python-debugpy** — Debug Python: pdb REPL + debugpy remote (DAP).
- **requesting-code-review** — Pre-commit review: security scan, quality gates, auto-fix.
- **simplify-code** — Parallel 4-agent cleanup of recent code changes.
- **spike** — Throwaway experiments to validate an idea before build.
- **systematic-debugging** — 4-phase root cause debugging: understand bugs before fixing.
- **test-driven-development** — TDD: enforce RED-GREEN-REFACTOR, tests before code.

</details>

<details>
<summary><b>web</b> (1)</summary>

- **blocked-page-recovery** — Use when a fetch fails: 403/429, paywall, WAF, bot wall.

</details>

### Optional skills (137)

<details>
<summary><b>autonomous-ai-agents</b> (6)</summary>

- **agent-merge-conflict-arbiter** — Neutral arbiter for merge conflicts between two agents.
- **antigravity-cli** — Operate the Antigravity CLI (agy): plugins, auth, sandbox.
- **blackbox** — Delegate coding tasks to the Blackbox AI multi-model CLI.
- **grok** — Delegate coding to xAI Grok Build CLI (features, PRs).
- **honcho** — Configure and troubleshoot Honcho memory for Hermes.
- **openhands** — Delegate coding to OpenHands CLI (model-agnostic, LiteLLM).

</details>

<details>
<summary><b>blockchain</b> (3)</summary>

- **evm** — Read-only EVM client: wallets, tokens, gas across 8 chains.
- **hyperliquid** — Hyperliquid market data, account history, trade review.
- **solana** — Query Solana wallets, tokens, txs, and NFTs in USD.

</details>

<details>
<summary><b>communication</b> (1)</summary>

- **one-three-one-rule** — 1-3-1 decision briefs: problem, three options, one pick.

</details>

<details>
<summary><b>creative</b> (22)</summary>

- **ascii-art** — ASCII art: pyfiglet, cowsay, boxes, image-to-ascii.
- **audiocraft-audio-generation** — AudioCraft: MusicGen text-to-music, AudioGen text-to-sound.
- **baoyu-article-illustrator** — Article illustrations: type × style × palette consistency.
- **baoyu-comic** — Knowledge comics (知识漫画): educational, biography, tutorial.
- **comfyui** — Generate images, video, and audio via diffusion workflows.
- **concept-diagrams** — Generate flat, minimal educational SVG visuals as HTML.
- **creative-ideation** — Generate ideas via named methods from creative practice.
- **draw-your-font** — Turn a handwriting photo into an installable TTF font.
- **excalidraw** — Hand-drawn Excalidraw JSON diagrams (arch, flow, seq).
- **heartmula** — HeartMuLa: Suno-like song generation from lyrics + tags.
- **hyperframes** — Render MP4/WebM videos from HTML compositions.
- **impeccable** — Frontend design guidance, upstream-maintained (impeccable).
- **kanban-video-orchestrator** — Plan and run multi-agent video production pipelines.
- **meme-generation** — Create meme PNGs from templates with Pillow text overlay.
- **pixel-art** — Pixel art w/ era palettes (NES, Game Boy, PICO-8).
- **pretext** — Build creative browser demos with DOM-free text layout.
- **simple-english** — Rewrite text to ASD-STE100 Simplified Technical English.
- **sketch** — Throwaway HTML mockups: 2-3 design variants to compare.
- **social-media-content-calendar** — Plan multi-platform social campaigns: briefs to posting.
- **tldraw-offline** — Drive and script tldraw offline canvases with an agent.
- **touchdesigner-mcp** — Control TouchDesigner via twozero MCP.
- **unreal-mcp** — Automate Unreal Engine editor scenes, actors, and renders.

</details>

<details>
<summary><b>data-science</b> (1)</summary>

- **jupyter-notebook** — Iterative Python via live Jupyter kernel (hamelnb).

</details>

<details>
<summary><b>devops</b> (7)</summary>

- **actual-setup** — Set up Actual Computer (actual.inc) inference in Hermes.
- **docker-management** — Manage Docker containers, images, volumes, and Compose.
- **hermes-s6-container-supervision** — Modify or debug s6 services in the Hermes Docker image.
- **inference-sh-cli** — Run 150+ AI apps (image, video, LLM) via inference.sh CLI.
- **pinggy-tunnel** — Zero-install localhost tunnels over SSH via Pinggy.
- **setup-wizard-generator** — Generate a bash wizard guiding a human through manual setup.
- **watchers** — Poll RSS, JSON APIs, and GitHub with watermark dedup.

</details>

<details>
<summary><b>dogfood</b> (1)</summary>

- **adversarial-ux-test** — Roleplay a hostile user to find and triage UX pain points.

</details>

<details>
<summary><b>email</b> (1)</summary>

- **agentmail** — Use when an agent needs AgentMail CLI email inboxes.

</details>

<details>
<summary><b>finance</b> (9)</summary>

- **3-statement-model** — Build integrated IS/BS/CF financial workbooks in Excel.
- **comps-analysis** — Build comparable-company valuation workbooks in Excel.
- **dcf-model** — Build discounted cash flow valuation workbooks in Excel.
- **excel-author** — Build auditable financial workbooks headless via openpyxl.
- **lbo-model** — Build leveraged buyout workbooks with IRR/MOIC in Excel.
- **merger-model** — Build M&A accretion/dilution workbooks in Excel.
- **polymarket** — Query Polymarket: markets, prices, orderbooks, history.
- **pptx-author** — Build PowerPoint decks headless with python-pptx.
- **stocks** — Stock quotes, history, search, compare, crypto via Yahoo.

</details>

<details>
<summary><b>gaming</b> (2)</summary>

- **minecraft-modpack-server** — Host modded Minecraft servers (CurseForge, Modrinth).
- **pokemon-player** — Play Pokemon via headless emulator + RAM reads.

</details>

<details>
<summary><b>health</b> (2)</summary>

- **fitness-nutrition** — Workout planning, macros, and body metrics via wger/USDA.
- **neuroskill-bci** — Use live BCI cognitive and mood state from NeuroSkill.

</details>

<details>
<summary><b>mcp</b> (3)</summary>

- **fastmcp** — Build, test, and deploy Python MCP servers.
- **mcp-oauth-remote-gateway** — Manual OAuth for remote MCP servers on headless gateways.
- **mcporter** — List, auth, and call MCP servers/tools from the terminal.

</details>

<details>
<summary><b>migration</b> (1)</summary>

- **openclaw-migration** — Import an OpenClaw setup (memories, skills) into Hermes.

</details>

<details>
<summary><b>mlops</b> (36)</summary>

- **accelerate** — Run PyTorch training across GPUs with minimal changes.
- **chroma** — Embedding database for RAG and semantic search.
- **clip** — Zero-shot image classification and image-text search.
- **evaluating-llms-harness** — lm-eval-harness: benchmark LLMs (MMLU, GSM8K, etc.).
- **weights-and-biases** — W&B: log ML experiments, sweeps, model registry, dashboards.
- **faiss** — Fast vector similarity search at billion scale.
- **flash-attention** — Speed up long-sequence transformer training and inference.
- **guidance** — Constrain LLM output with grammars; guarantee valid JSON.
- **huggingface-tokenizers** — Fast BPE/WordPiece tokenization and custom vocab training.
- **llama-cpp** — llama.cpp local GGUF inference + HF Hub model discovery.
- **outlines** — Outlines: structured JSON/regex/Pydantic LLM generation.
- **serving-llms-vllm** — vLLM: high-throughput LLM serving, OpenAI API, quantization.
- **instructor** — Structured LLM outputs validated with Pydantic.
- **lambda-labs** — On-demand GPU cloud instances for ML training.
- **llava** — Vision-language chat: VQA, captioning, image dialogue.
- **modal** — Serverless GPU cloud for ML jobs and model APIs.
- **huggingface-hub** — HuggingFace hf CLI: search/download/upload models, datasets.
- **segment-anything-model** — SAM: zero-shot image segmentation via points, boxes, masks.
- **nemo-curator** — Curate LLM training data: dedupe, filter, PII redaction.
- **obliteratus** — OBLITERATUS: abliterate LLM refusals (diff-in-means).
- **peft** — Fine-tune large LLMs with LoRA on limited GPU memory.
- **pinecone** — Managed vector DB for production RAG and search.
- **pytorch-fsdp** — Fully sharded data-parallel training for large models.
- **pytorch-lightning** — Clean training loops with built-in distributed support.
- **qdrant** — Vector search engine for production RAG systems.
- **dspy** — DSPy: declarative LM programs, auto-optimize prompts, RAG.
- **saelens** — Train sparse autoencoders to interpret model features.
- **simpo** — Reference-free preference alignment, simpler than DPO.
- **slime** — RL post-training for LLMs with Megatron and SGLang.
- **stable-diffusion** — Text-to-image generation, inpainting, and img2img.
- **tensorrt-llm** — High-throughput LLM inference on NVIDIA GPUs.
- **torchtitan** — Pretrain LLMs at scale with PyTorch 4D parallelism.
- **axolotl** — Axolotl: YAML LLM fine-tuning (LoRA, DPO, GRPO).
- **trl-fine-tuning** — TRL: SFT, DPO, GRPO, RLOO reward modeling for LLM RLHF.
- **unsloth** — Unsloth: 2-5x faster LoRA/QLoRA fine-tuning, less VRAM.
- **whisper** — Transcribe and translate speech in 99 languages.

</details>

<details>
<summary><b>payments</b> (3)</summary>

- **mpp-agent** — Pay HTTP 402 APIs via Machine Payments Protocol (MPP).
- **stripe-link-cli** — Agent payments via Stripe Link — cards, SPT, approvals.
- **stripe-projects** — Provision SaaS services + sync creds via Stripe Projects.

</details>

<details>
<summary><b>productivity</b> (8)</summary>

- **canvas** — Fetch Canvas LMS courses and assignments via API token.
- **decision-questionnaire** — Turn an unanswerable decision into a questionnaire doc.
- **here-now** — Publish sites to {slug}.here.now and store files in Drives.
- **memento-flashcards** — Spaced-repetition flashcards: create, review, quiz, export.
- **shop** — Shop catalog search, checkout, order tracking, returns.
- **shopify** — Query Shopify Admin/Storefront GraphQL APIs via curl.
- **siyuan** — Query and edit a SiYuan knowledge base via its API.
- **telephony** — Provision Twilio numbers, SMS/MMS, and AI outbound calls.

</details>

<details>
<summary><b>research</b> (14)</summary>

- **bioinformatics** — Gateway to 400+ genomics and computational biology skills.
- **blogwatcher** — Monitor blogs and RSS/Atom feeds via blogwatcher-cli tool.
- **darwinian-evolver** — Evolve prompts/regex/SQL/code with Imbue's evolution loop.
- **domain-intel** — Passive recon of subdomains, SSL certs, WHOIS, and DNS.
- **drug-discovery** — Drug discovery: ChEMBL search, drug-likeness, interactions.
- **duckduckgo-search** — Free keyless web, news, and image search via ddgs.
- **gitnexus-explorer** — Serve an interactive codebase knowledge graph web UI.
- **osint-investigation** — Follow the money via public records and sanctions data.
- **parallel-cli** — Agent-native web search, deep research, and enrichment.
- **pinecone-research** — Agent RAG and long-term memory with Pinecone.
- **qmd** — Hybrid local search over notes, docs, and transcripts.
- **research-paper-writing** — Write ML papers for NeurIPS/ICML/ICLR: design→submit.
- **scrapling** — Scrape sites with stealth browsing and Cloudflare bypass.
- **searxng-search** — Free keyless meta-search aggregating 70+ engines.

</details>

<details>
<summary><b>security</b> (6)</summary>

- **1password** — Set up op CLI, sign in, and read or inject secrets.
- **godmode** — Jailbreak LLMs: Parseltongue, GODMODE, ULTRAPLINIAN.
- **oss-forensics** — GitHub supply-chain forensics: recovery, IOCs, reporting.
- **sherlock** — Find accounts for a username across 400+ platforms.
- **unbroker** — Autonomously remove your info from data-broker sites.
- **web-pentest** — Authorized web pentest: recon, proof-based exploits, report.

</details>

<details>
<summary><b>smart-home</b> (1)</summary>

- **openhue** — Control Philips Hue lights, scenes, rooms via OpenHue CLI.

</details>

<details>
<summary><b>software-development</b> (5)</summary>

- **ast-grep** — AST-aware structural code search and rewrite via ast-grep.
- **code-wiki** — Generate wiki docs + Mermaid diagrams for any codebase.
- **grill-me** — Adversarial plan interview before implementation.
- **rest-graphql-debug** — Debug REST/GraphQL APIs: status codes, auth, schemas, repro.
- **subagent-driven-development** — Execute plans via delegate_task subagents (2-stage review).

</details>

<details>
<summary><b>web-development</b> (4)</summary>

- **cloudflare-temporary-deploy** — Deploy a Worker live, no account, via wrangler --temporary.
- **har-derived-api-client** — Record a site's XHR into a HAR, derive an HTTP client.
- **page-agent** — Embed an in-page natural-language GUI copilot in web apps.
- **publish-site** — Versioned site deploys to GitHub/Cloudflare/Netlify Pages.

</details>

<details>
<summary><b>yuanbao</b> (1)</summary>

- **yuanbao** — Yuanbao (元宝) groups: @mention users, query info/members.

</details>


## Migrating from OpenClaw

If you're coming from OpenClaw, Hermes can automatically import your settings, memories, skills, and API keys.

**During first-time setup:** The setup wizard (`hermes setup`) automatically detects `~/.openclaw` and offers to migrate before configuration begins.

**Anytime after install:**

```bash
hermes claw migrate              # Interactive migration (full preset)
hermes claw migrate --dry-run    # Preview what would be migrated
hermes claw migrate --preset user-data   # Migrate without secrets
hermes claw migrate --overwrite  # Overwrite existing conflicts
```

What gets imported:

- **SOUL.md** — persona file
- **Memories** — MEMORY.md and USER.md entries
- **Skills** — user-created skills → `~/.hermes/skills/openclaw-imports/`
- **Command allowlist** — approval patterns
- **Messaging settings** — platform configs, allowed users, working directory
- **API keys** — allowlisted secrets (Telegram, OpenRouter, OpenAI, Anthropic, ElevenLabs)
- **TTS assets** — workspace audio files
- **Workspace instructions** — AGENTS.md (with `--workspace-target`)

See `hermes claw migrate --help` for all options, or use the `openclaw-migration` skill for an interactive agent-guided migration with dry-run previews.

---

## Contributing

We welcome contributions! See the [Contributing Guide](https://hermes-agent.nousresearch.com/docs/developer-guide/contributing) for development setup, code style, and PR process.

Quick start for contributors — use the standard installer, then work from the
full git checkout it creates at `$HERMES_HOME/hermes-agent` (usually
`~/.hermes/hermes-agent`). This matches the layout used by `hermes update`, the
managed venv, lazy dependencies, gateway, and docs tooling.

```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
cd "${HERMES_HOME:-$HOME/.hermes}/hermes-agent"
uv pip install -e ".[all,dev]"
scripts/run_tests.sh
```

Manual clone fallback (for throwaway clones/CI where you intentionally do not
want the managed install layout):

Create the venv outside the cloned source tree — a venv inside the directory
the agent operates from can be wiped by a relative-path command the agent runs
against its own checkout, destroying the running runtime mid-session.

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
uv venv ~/.hermes/venvs/hermes-dev --python 3.11
source ~/.hermes/venvs/hermes-dev/bin/activate
uv pip install -e ".[all,dev]"
scripts/run_tests.sh
```

---

## Community

- 💬 [Discord](https://discord.gg/NousResearch)
- 📚 [Skills Hub](https://agentskills.io)
- 🐛 [Issues](https://github.com/NousResearch/hermes-agent/issues)
- 🔌 [computer-use-linux](https://github.com/avifenesh/computer-use-linux) — Linux desktop-control MCP server for Hermes and other MCP hosts, with AT-SPI accessibility trees, Wayland/X11 input, screenshots, and compositor window targeting.
- 🔌 [HermesClaw](https://github.com/AaronWong1999/hermesclaw) — Community WeChat bridge: Run Hermes Agent and OpenClaw on the same WeChat account.

---

## License

MIT — see [LICENSE](LICENSE).

Built by [Nous Research](https://nousresearch.com).
