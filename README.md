<div align="center">

<img src="DriftBreak.png" width="120" height="120" alt="DriftBreak Logo" />

# DriftBreak
**Context Pruning & State-Extraction Scaffold for Local LLMs**

[![Release](https://img.shields.io/badge/Release-v1.5.0--GOLD--SESSIONS-blue.svg)](https://github.com/Recursive-Logic-Core/DriftBreak/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Localhost Only](https://img.shields.io/badge/Network-127.0.0.1%20Only-green.svg)]()

<br />

<a href="https://github.com/Recursive-Logic-Core/DriftBreak/releases/latest/download/DriftBreak.exe">
  <img src="https://img.shields.io/badge/⬇️_DOWNLOAD_EXE-Windows_Standalone_(x64)-2563eb?style=for-the-badge&logo=windows&logoColor=white" alt="Download DriftBreak.exe" />
</a>

<p><em>Standalone reference tool — No Python installation required.</em></p>

</div>

---

### What this project is (and what it is not)

**This is an architectural skeleton and proof-of-concept, not a turnkey enterprise product.**

When running long sessions with local LLMs, chat histories expand rapidly. This leads to context drift and excessive memory consumption. DriftBreak demonstrates a minimal, working pattern to counter this: extracting a structured summary (**State + Glossary**) from the active conversation and discarding the raw, bloated history in favor of a lean recovery payload.

* **For everyday users:** A compiled `.exe` is provided to test this state-recovery concept out of the box on localhost.
* **For developers & organizations:** This repository serves as a functional blueprint. It demonstrates the baseline logic. Teams integrating this mechanism into production pipelines are expected to take these core concepts and adapt them to their specific infrastructure (custom token counters, enterprise database layers, concurrent multi-user locks).

---

### Core Mechanics in the Script

1. **Input Ingestion:** Reads the conversation log from `session_input.txt`.
2. **Turn Splitting:** Parses text sequentially into distinct turns using `USER:` and `ASSISTANT:` markers.
3. **Structured Extraction:** Prompts the local model (Ollama, LM Studio, or OpenAI-compatible local endpoints) using strict system instructions to isolate:
   * `State`: Active constraints, established facts, and current project context.
   * `Glossary`: Project-specific terminology and definitions (merged incrementally across runs).
4. **Payload Assembly:** Generates `pruned_context_payload.json` containing the extracted state, updated glossary, and a user-selected number of recent turns (`keep_prompts`).
5. **Session Vault & Atomic Persistence:** Backs up raw text inputs and stores JSON artifacts in sequential session folders (`sessions/00001/`, `sessions/00002/`). Uses temporary file replacement (`os.replace`) to prevent file corruption during manual interrupts.

---

### Scope & Practical Boundaries

To maintain technical clarity regarding this reference implementation:

* **Turn-Based Pruning:** Context retention is governed by turn count (`keep_prompts`), not dynamic token-window calculations.
* **Hardware Telemetry:** GPU memory queries (`nvidia-smi`) operate strictly as an informational readout in this build; the script does not actively throttle execution based on memory thresholds.
* **Format Dependency:** The extraction loop relies on the local model returning valid JSON. If the model outputs malformed syntax, the script falls back to an empty baseline state.
* **Execution Scope:** Designed as an offline, single-user desktop utility and architectural scaffold.

---

### Quick Start

**Using the Standalone Executable:**
1. Download `DriftBreak.exe`.
2. Place your chat log into `session_input.txt` in the same directory.
3. Run `DriftBreak.exe`, select your local model node, and choose your retention depth.
4. Use the generated `pruned_context_payload.json` from the `sessions/` directory to continue your work with clean context.

**Running from Source:**
```bash
git clone [https://github.com/Recursive-Logic-Core/DriftBreak.git](https://github.com/Recursive-Logic-Core/DriftBreak.git)
cd DriftBreak
pip install requests
python DriftBreak.py
```

## Contact & Architecture Core
Developed and maintained by **Architect M.M.M.**  
Direct contact: `arch_mmm@proton.me`
