**Key Features**
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

## Quick Start

1. **Clone the repository**

   ```bash
   git clone https://github.com/<your-username>/Memory.dll.git
   cd Memory.dll
   ```
2. **Open** `Memory.sln` in Visual Studio (2019 or 2022)
3. **Build** the `Memory` project to produce `Memory.dll`
4. **Reference** `Memory.dll` in your application and use:

   ```csharp
   using Memory;

   var mem = new Mem();
   if (!mem.OpenProcess("notepad.exe", out var error))
       throw new Exception($"Failed to open process: {error}");

   // Read 16 bytes from address computed via pointer offsets
   UIntPtr addr = mem.GetCode("main+0x1234,0x8", "", size:16);
   byte[] buffer = new byte[16];
   Imps.ReadProcessMemory(mem.mProc.Handle, addr, buffer, (UIntPtr)buffer.Length, IntPtr.Zero);
   Console.WriteLine("Data: " + Mem.ByteArrayToHexString(buffer));
   ```

---

## Requirements

* Windows 7 or later
* .NET Framework 4.6.1+ or .NET 8
