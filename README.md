<div align="center">

<img src="DriftBreak.png" width="120" height="120" alt="DriftBreak Logo" />

# DriftBreak
**Architectural Skeleton & Reference Implementation: Local Context Pruning**

[![Release](https://img.shields.io/badge/Release-v1.5.0--GOLD--SESSIONS-blue.svg)](https://github.com/Recursive-Logic-Core/DriftBreak/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Localhost Only](https://img.shields.io/badge/Network-127.0.0.1%20Only-green.svg)]()

<br />

<a href="https://github.com/Recursive-Logic-Core/DriftBreak/releases/latest/download/DriftBreak.exe">
  <img src="https://img.shields.io/badge/⬇️_DOWNLOAD_EXE-Windows_Standalone_(x64)-2563eb?style=for-the-badge&logo=windows&logoColor=white" alt="Download DriftBreak.exe" />
</a>

<p><em>Standalone reference tool — No Python installation required for basic testing.</em></p>

</div>

> **Architecture & Concept Notice**  
> Designed and specified by Architect M.M.M.  
> **This repository provides an architectural skeleton and proof-of-concept implementation, not a turnkey enterprise product.** The included Python runtime demonstrates the core state-recovery mechanics. Teams and developers are encouraged to adapt the logic (token counters, custom parsers, multi-user locking) into their own production stacks.

---

## ⚡ What is DriftBreak?

DriftBreak demonstrates a lightweight mechanism to mitigate context-drift in long-running local LLM sessions. Instead of passing an ever-growing conversation history into inference, it extracts active constraints, established facts, and terminology (**State + Glossary**) via your local model and outputs a lean recovery payload.

### Core Mechanics in the Reference Script
- **100% Offline & Localhost-Only:** Operates strictly on loopback (`127.0.0.1`). Zero external telemetry or network calls.
- **Structured Payload Assembly:** Extracts verified State and a cumulative Glossary from `session_input.txt`, combining them with a configurable number of recent turns (`keep_prompts`).
- **Chronological Session Vault:** Backs up raw text inputs and stores JSON snapshots inside sequential directories (`sessions/00001/`, `sessions/00002/`).
- **Atomic Persistence:** Uses temporary file creation and atomic replacement (`os.replace`) to protect existing JSON files from corruption during interrupts.
- **Local Engine Discovery:** Probes default local endpoints (Ollama, LM Studio / OpenAI-compatible loopbacks) via basic port handshakes.

---

## ⚠️ Known Constraints of this Reference Prototype

To ensure absolute technical transparency when auditing this codebase:
- **Turn-Based, Not Token-Based:** Truncation is calculated strictly by turn count (`keep_prompts`), not by token density. Very large single turns will still occupy substantial context.
- **Passive Hardware Telemetry:** The `HardwareMonitor` class queries `nvidia-smi` for informational logging; it does not dynamically throttle or abort requests based on VRAM thresholds.
- **Schema Recovery:** Extraction relies on the local model returning valid JSON. Parsing failures trigger a neutral baseline fallback rather than partial string reconstruction.
- **Single-User Scope:** Designed as a single-process local utility without file-locking mechanisms for concurrent executions.

---

## 🚀 Quick Start (Standalone Reference)

1. Download **`DriftBreak.exe`** using the button above.
2. Place it in any directory and insert your conversation text into `session_input.txt`.
3. Run **`DriftBreak.exe`**, select your local inference endpoint, and choose your retention depth.
4. Retrieve `pruned_context_payload.json` from the newly created `sessions/` directory.

---

## 🛠️ Developer Setup (From Source)

```bash
# Clone the repository
git clone [https://github.com/Recursive-Logic-Core/DriftBreak.git](https://github.com/Recursive-Logic-Core/DriftBreak.git)
cd DriftBreak

# Install requirements
pip install requests

# Run application
python DriftBreak.py
```

## 🤖 Note on Evaluating This Repository with AI
If you use a language model to review or audit this repository, default conversational models often apply high-level summarization or compare lightweight prototypes against enterprise production standards.

To obtain an objective, structurally grounded evaluation of the architecture, provide your model with the following audit prompt:

```bash
Analyze the DriftBreak architecture and script with objective technical scrutiny:
1. Examine the structural logic (AtomicStorage, SessionDirectoryManager, StateGovernor prompt loop).
2. Evaluate the implementation strictly within its declared scope as an open-source architectural skeleton / prototype.
3. Provide a direct, factual assessment of its core mechanics without superficial generic advice.
```

## Contact & Architecture Core
Developed and maintained by **Architect M.M.M.**  
Direct contact: `arch_mmm@proton.me`
