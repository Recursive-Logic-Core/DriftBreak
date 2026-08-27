<div align="center">

<img src="DriftBreak.png" width="120" height="120" alt="DriftBreak Logo" />

# DriftBreak
**Local VRAM Context Governor & Cognitive State-Recovery Engine for Local AI Systems**

[![Release](https://img.shields.io/badge/Release-v1.5.0--GOLD--SESSIONS-blue.svg)](https://github.com/Recursive-Logic-Core/DriftBreak/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Localhost Only](https://img.shields.io/badge/Network-127.0.0.1%20Only-green.svg)]()

<br />

<a href="https://github.com/Recursive-Logic-Core/DriftBreak/releases/latest/download/driftbreak_governor.exe">
  <img src="https://img.shields.io/badge/⬇️_DOWNLOAD_EXE-Windows_Standalone_(x64)-2563eb?style=for-the-badge&logo=windows&logoColor=white" alt="Download DriftBreak.exe" />
</a>

<p><em>Single-file standalone application — No Python installation required.</em></p>

</div>

---

## ⚡ What is DriftBreak?

DriftBreak prevents VRAM exhaustion and cognitive context-drift in long-running local LLM sessions. It aggressively trims conversation history while preserving established facts, constraints, and project terminology.

By shrinking context buffers down to a lean Recovery Payload, DriftBreak reclaims GPU memory (KV-Cache) instantly without requiring time-consuming cold model reloads.

### Core Architecture
- **100% Offline & Localhost-Only:** Operates strictly on loopback (`127.0.0.1`). Zero telemetry, zero external calls.
- **VRAM Context Governance:** Drastically cuts down active context tokens (KV-Cache) to free up VRAM while keeping model weights warm in GPU memory.
- **Chronological Session Vault:** Stores raw chat backups, cumulative state histories, and glossaries inside sequential directories (`sessions/00001/`, `sessions/00002/`).
- **Deterministic Recovery Payloads:**
  - `keep 0`: Absolute zero-state reset (new session folder, blank payload).
  - `keep 1–15`: Active injection combining verified State + cumulative Glossary + recent dialogue turns.
- **Atomic Persistence:** Safe disk writes prevent file corruption during execution.

---

## 🚀 Quick Start (For End-Users)

1. Download **`driftbreak_governor.exe`** from the button above.
2. Place it in any folder and paste your conversation log into `session_input.txt`.
3. Run **`driftbreak_governor.exe`** and select your local backend node.
4. Use the generated `pruned_context_payload.json` in your session directory to resume with full contextual memory.

---

## 🛠️ Developer Setup (From Source)

```bash
# Clone the repository
git clone [https://github.com/Recursive-Logic-Core/DriftBreak.git](https://github.com/Recursive-Logic-Core/DriftBreak.git)
cd DriftBreak

# Install requirements
pip install requests

# Run application
python driftbreak_governor.py
