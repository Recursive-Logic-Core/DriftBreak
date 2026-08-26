<div align="center">

<img src="DriftBreak.png" width="120" height="120" alt="DriftBreak Logo" />

# DriftBreak
**Local VRAM Governor & Cognitive State-Recovery Engine for Local AI Systems**

[![Release](https://img.shields.io/badge/Release-v1.4.0--GOVERNOR-blue.svg)](https://github.com/Recursive-Logic-Core/DriftBreak/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Localhost Only](https://img.shields.io/badge/Network-127.0.0.1%20Only-green.svg)]()

<br />

<a href="https://github.com/Recursive-Logic-Core/DriftBreak/releases/latest/download/DriftBreak.exe">
  <img src="https://img.shields.io/badge/⬇️_DOWNLOAD_EXE-Windows_Standalone_(x64)-2563eb?style=for-the-badge&logo=windows&logoColor=white" alt="Download DriftBreak.exe" />
</a>

<p><em>Single-file standalone application — No Python installation required.</em></p>

</div>

---

## ⚡ What is DriftBreak?

DriftBreak is a lightweight, purely local tool that preserves memory and extracts established facts, constraints, and project terminology before executing a VRAM flush. 

It ensures that when a local AI engine or pipeline is reloaded or restarted, it resumes instantly with full contextual awareness instead of resetting to a blank baseline.

### Core Architecture
- **100% Offline & Localhost-Only:** Runs strictly on loopback (`127.0.0.1`). No telemetry, no external calls.
- **Active Memory Flushing:** Explicitly unloads models from GPU memory (`keep_alive: 0`) after saving checkpoints.
- **Cumulative Glossary:** Aggregates and deduplicates domain-specific terms across sessions without data loss.
- **Atomic Persistence:** Safeguards all recovery states against process corruption.

---

## 🚀 Quick Start (For End-Users)

1. Download **`DriftBreak.exe`** from the button above.
2. Place it in any folder and paste your active conversation log into `session_input.txt`.
3. Run **`DriftBreak.exe`** and select your local backend.
4. Copy the generated `pruned_context_payload.json` into your next session to resume work with complete memory.

---

## 🛠️ Developer Setup (From Source)

```bash
# Clone the repository
git clone https://github.com/Recursive-Logic-Core/DriftBreak.git
cd DriftBreak

# Install requirements
pip install requests

# Run application
python DriftBreak.py
