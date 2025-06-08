## Key Features
* **Process Management**

  * Open/close processes by name or PID
  * Check 32‑bit vs. 64‑bit automatically
* **Memory Operations**

  * Read and write process memory with support for complex pointer chains
  * `VirtualQueryEx` wrapper for querying memory regions
  * Full process memory dumping to file
* **Code Injection & Patching**

  * Inject a DLL via remote thread + `VirtualAllocEx`
  * Create code caves and apply in‑memory patches
* **Thread Control**

  * Suspend/resume entire processes or individual threads
  * Query thread start addresses via `NtQueryInformationThread`
* **Utilities**

  * Convert byte arrays to hex/string representations
  * Named pipe client helper for IPC
  * Asynchronous delays, file‑to‑byte conversions, and more

---

## Requirements

* Windows 7 or later
* .NET Framework 4.6.1+ or .NET 8
