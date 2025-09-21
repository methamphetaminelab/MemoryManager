# MemoryManager

MemoryManager - это библиотека C#, предназначенная для взаимодействия с памятью других процессов, позволяющая читать, записывать, сканировать память, внедрять DLL и управлять потоками.

## Функции

### Общие функции
- `OpenProcess(int pid, out string FailReason)`: Открывает процесс по его идентификатору (PID).
- `OpenProcess(string proc, out string FailReason)`: Открывает процесс по имени.
- `OpenProcess(string proc)`: Открывает процесс по имени (без причины сбоя).
- `OpenProcess(int pid)`: Открывает процесс по его идентификатору (без причины сбоя).
- `CloseProcess()`: Закрывает открытый процесс.
- `GetProcIdFromName(string name)`: Получает идентификатор процесса (PID) по его имени.
- `SetFocus()`: Устанавливает фокус на главное окно открытого процесса.
- `LoadCode(string name, string iniFile)`: Загружает код из INI-файла.
- `ThreadStartClient(string func, string name)`: Запускает клиент именованного канала для выполнения функции.
- `GetCode(string name, string path = "", int size = 8)`: Получает адрес памяти на основе имени, пути и размера.
- `Get64BitCode(string name, string path = "", int size = 16)`: Получает 64-битный адрес памяти на основе имени, пути и размера.
- `GetModuleAddressByName(string name)`: Получает базовый адрес модуля по его имени.
- `InjectDll(String strDllName)`: Внедряет DLL в открытый процесс.
- `CreateCodeCave(UIntPtr address, byte[] newBytes, int replaceCount, int size = 0x1000)`: Создает "Code Cave" для выполнения пользовательского кода.
- `SuspendProcess(int pid)`: Приостанавливает выполнение процесса по PID.
- `ResumeProcess(int pid)`: Возобновляет выполнение процесса по PID.
- `AppendAllBytes(string path, byte[] bytes)`: Добавляет массив байтов к файлу.
- `FileToBytes(string path, bool dontDelete = false)`: Преобразует файл в массив байтов.
- `MSize()`: Возвращает "x16" для 64-битных систем и "x8" для 32-битных.
- `ByteArrayToHexString(byte[] ba)`: Преобразует массив байтов в шестнадцатеричную строку.
- `ByteArrayToString(byte[] ba)`: Преобразует массив байтов в строковое представление.
- `GetMinAddress()`: Получает минимальный адрес приложения.
- `DumpMemory(string file = "dump.dmp")`: Дамп памяти процесса в файл.
- `GetThreads()`: Выводит информацию о потоках процесса в отладочную консоль.
- `GetThreadStartAddress(int threadId)`: Получает начальный адрес потока по его ID.
- `SuspendThreadByID(int ThreadID)`: Приостанавливает выполнение потока по его ID.

### Функции сканирования (AoB.cs)
- `AoBScan(string search, bool writable = false, bool executable = true, string file = "")`: Асинхронно сканирует память на предмет Array of Bytes (AoB).
- `AoBScan(string search, bool readable, bool writable, bool executable, string file = "")`: Асинхронно сканирует память с указанием прав доступа.
- `AoBScan(long start, long end, string search, bool writable = false, bool executable = true, bool mapped = false, string file = "")`: Асинхронно сканирует заданный диапазон памяти.
- `AoBScan(long start, long end, string search, bool readable, bool writable, bool executable, bool mapped, string file = "")`: Асинхронно сканирует заданный диапазон памяти с указанием прав доступа.
- `AoBScan(string code, long end, string search, string file = "")`: Асинхронно сканирует память, начиная с адреса, полученного из кода.

### Функции чтения (Read.cs)
- `CutString(string str)`: Обрезает строку до первого непечатаемого символа.
- `ReadBytes(string code, long length, string file = "")`: Читает указанное количество байтов из памяти по заданному адресу.
- `ReadFloat(string code, string file = "", bool round = true)`: Читает значение типа `float` из памяти.
- `ReadString(string code, string file = "", int length = 32, bool zeroTerminated = true, System.Text.Encoding stringEncoding = null)`: Читает строку из памяти.
- `ReadDouble(string code, string file = "", bool round = true)`: Читает значение типа `double` из памяти.
- `ReadUIntPtr(UIntPtr code)`: Читает значение типа `UIntPtr` из памяти.
- `ReadInt(string code, string file = "")`: Читает значение типа `int` из памяти.
- `ReadLong(string code, string file = "")`: Читает значение типа `long` из памяти.
- `ReadUInt(string code, string file = "")`: Читает значение типа `UInt32` из памяти.
- `Read2ByteMove(string code, int moveQty, string file = "")`: Читает 2 байта со смещением от заданного адреса.
- `ReadIntMove(string code, int moveQty, string file = "")`: Читает `int` со смещением от заданного адреса.
- `ReadUIntMove(string code, int moveQty, string file = "")`: Читает `ulong` со смещением от заданного адреса.
- `Read2Byte(string code, string file = "")`: Читает 2 байта из памяти.
- `ReadByte(string code, string file = "")`: Читает 1 байт из памяти.
- `ReadBits(string code, string file = "")`: Читает биты из 1 байта памяти.
- `ReadPByte(UIntPtr address, string code, string file = "")`: Читает байт из памяти по указателю с относительным смещением.
- `ReadPFloat(UIntPtr address, string code, string file = "")`: Читает `float` из памяти по указателю с относительным смещением.
- `ReadPInt(UIntPtr address, string code, string file = "")`: Читает `int` из памяти по указателю с относительным смещением.
- `ReadPString(UIntPtr address, string code, string file = "")`: Читает строку из памяти по указателю с относительным смещением.
- `ReadMemory<T>(string address, string file = "")`: Универсальная функция для чтения данных различных типов из памяти.
- `BindToUI<T>(string address, Action<string> UIObject, string file = "")`: Привязывает чтение значения из памяти к обновлению элемента пользовательского интерфейса.

### Функции записи (Write.cs)
- `FreezeValue(string address, string type, string value, string file = "")`: "Замораживает" значение по адресу памяти, постоянно записывая его.
- `UnfreezeValue(string address)`: Размораживает значение по адресу памяти.
- `WriteMemory(string code, string type, string write, string file = "", System.Text.Encoding stringEncoding = null, bool RemoveWriteProtection = true)`: Записывает значение указанного типа по заданному адресу памяти.
- `WriteMove(string code, string type, string write, int MoveQty, string file = "", int SlowDown = 0)`: Записывает значение со смещением от заданного адреса.
- `WriteBytes(string code, byte[] write, string file = "")`: Записывает массив байтов по заданному адресу памяти.
- `WriteBits(string code, bool[] bits, string file = "")`: Записывает биты в 1 байт памяти.
- `WriteBytes(UIntPtr address, byte[] write)`: Записывает массив байтов по указанному адресу памяти.

---

# MemoryManager

MemoryManager is a C# library designed for interacting with the memory of other processes, allowing you to read, write, scan memory, inject DLLs, and manage threads.

## Functions

### General Functions
- `OpenProcess(int pid, out string FailReason)`: Opens a process by its Process ID (PID).
- `OpenProcess(string proc, out string FailReason)`: Opens a process by name.
- `OpenProcess(string proc)`: Opens a process by name (without failure reason).
- `OpenProcess(int pid)`: Opens a process by its Process ID (without failure reason).
- `CloseProcess()`: Closes the opened process.
- `GetProcIdFromName(string name)`: Gets the Process ID (PID) from its name.
- `SetFocus()`: Sets focus to the main window of the opened process.
- `LoadCode(string name, string iniFile)`: Loads code from an INI file.
- `ThreadStartClient(string func, string name)`: Starts a named pipe client to execute a function.
- `GetCode(string name, string path = "", int size = 8)`: Gets a memory address based on name, path, and size.
- `Get64BitCode(string name, string path = "", int size = 16)`: Gets a 64-bit memory address based on name, path, and size.
- `GetModuleAddressByName(string name)`: Gets the base address of a module by its name.
- `InjectDll(String strDllName)`: Injects a DLL into the opened process.
- `CreateCodeCave(UIntPtr address, byte[] newBytes, int replaceCount, int size = 0x1000)`: Creates a "Code Cave" to execute custom code.
- `SuspendProcess(int pid)`: Suspends process execution by PID.
- `ResumeProcess(int pid)`: Resumes process execution by PID.
- `AppendAllBytes(string path, byte[] bytes)`: Appends a byte array to a file.
- `FileToBytes(string path, bool dontDelete = false)`: Converts a file to a byte array.
- `MSize()`: Returns "x16" for 64-bit systems and "x8" for 32-bit systems.
- `ByteArrayToHexString(byte[] ba)`: Converts a byte array to a hexadecimal string.
- `ByteArrayToString(byte[] ba)`: Converts a byte array to a string representation.
- `GetMinAddress()`: Gets the minimum application address.
- `DumpMemory(string file = "dump.dmp")`: Dumps process memory to a file.
- `GetThreads()`: Outputs process thread information to the debug console.
- `GetThreadStartAddress(int threadId)`: Gets the start address of a thread by its ID.
- `SuspendThreadByID(int ThreadID)`: Suspends thread execution by its ID.

### Scanning Functions (AoB.cs)
- `AoBScan(string search, bool writable = false, bool executable = true, string file = "")`: Asynchronously scans memory for an Array of Bytes (AoB).
- `AoBScan(string search, bool readable, bool writable, bool executable, string file = "")`: Asynchronously scans memory with specified access rights.
- `AoBScan(long start, long end, string search, bool writable = false, bool executable = true, bool mapped = false, string file = "")`: Asynchronously scans a specified memory range.
- `AoBScan(long start, long end, string search, bool readable, bool writable, bool executable, bool mapped, string file = "")`: Asynchronously scans a specified memory range with specified access rights.
- `AoBScan(string code, long end, string search, string file = "")`: Asynchronously scans memory starting from an address obtained from code.

### Reading Functions (Read.cs)
- `CutString(string str)`: Truncates a string at the first non-printable character.
- `ReadBytes(string code, long length, string file = "")`: Reads a specified number of bytes from memory at a given address.
- `ReadFloat(string code, string file = "", bool round = true)`: Reads a `float` value from memory.
- `ReadString(string code, string file = "", int length = 32, bool zeroTerminated = true, System.Text.Encoding stringEncoding = null)`: Reads a string from memory.
- `ReadDouble(string code, string file = "", bool round = true)`: Reads a `double` value from memory.
- `ReadUIntPtr(UIntPtr code)`: Reads a `UIntPtr` value from memory.
- `ReadInt(string code, string file = "")`: Reads an `int` value from memory.
- `ReadLong(string code, string file = "")`: Reads a `long` value from memory.
- `ReadUInt(string code, string file = "")`: Reads a `UInt32` value from memory.
- `Read2ByteMove(string code, int moveQty, string file = "")`: Reads 2 bytes with an offset from a given address.
- `ReadIntMove(string code, int moveQty, string file = "")`: Reads an `int` with an offset from a given address.
- `ReadUIntMove(string code, int moveQty, string file = "")`: Reads a `ulong` with an offset from a given address.
- `Read2Byte(string code, string file = "")`: Reads 2 bytes from memory.
- `ReadByte(string code, string file = "")`: Reads 1 byte from memory.
- `ReadBits(string code, string file = "")`: Reads bits from 1 byte of memory.
- `ReadPByte(UIntPtr address, string code, string file = "")`: Reads a byte from memory at a pointer with a relative offset.
- `ReadPFloat(UIntPtr address, string code, string file = "")`: Reads a `float` from memory at a pointer with a relative offset.
- `ReadPInt(UIntPtr address, string code, string file = "")`: Reads an `int` from memory at a pointer with a relative offset.
- `ReadPString(UIntPtr address, string code, string file = "")`: Reads a string from memory at a pointer with a relative offset.
- `ReadMemory<T>(string address, string file = "")`: Universal function for reading various data types from memory.
- `BindToUI<T>(string address, Action<string> UIObject, string file = "")`: Binds reading a value from memory to updating a UI element.

### Writing Functions (Write.cs)
- `FreezeValue(string address, string type, string value, string file = "")`: "Freezes" a value at a memory address by continuously writing to it.
- `UnfreezeValue(string address)`: Unfreezes a value at a memory address.
- `WriteMemory(string code, string type, string write, string file = "", System.Text.Encoding stringEncoding = null, bool RemoveWriteProtection = true)`: Writes a value of the specified type to a given memory address.
- `WriteMove(string code, string type, string write, int MoveQty, string file = "", int SlowDown = 0)`: Writes a value with an offset from a given address.
- `WriteBytes(string code, byte[] write, string file = "")`: Writes a byte array to a given memory address.
- `WriteBits(string code, bool[] bits, string file = "")`: Writes bits to 1 byte of memory.
- `WriteBytes(UIntPtr address, byte[] write)`: Writes a byte array to a specified memory address.
