# Unsigned Driver Mapper for Windows 10/11

An **Unsigned Driver Mapper** for Windows 10 22H2 → Windows 11 23H2 that leverages **PdFwKrnl** to exploit Read/Write IOCTL calls to temporarily disable **DSE & PatchGuard** and map unsigned drivers.  

*(Original GitHub repo got deleted, and this is a repost to keep the mapper available.)*

---

## Features

- Maps **unsigned drivers** on Windows 10/11.  
- Uses **PdFwKrnl** for kernel-level IOCTL exploitation.  
- Disables **DSE** (Driver Signature Enforcement) and **PatchGuard** temporarily.  
- Fully tested on **BattleEye-protected games**: Escape from Tarkov, DayZ, Rainbow Six Siege.  

---

## Usage Example

```cpp
#include <iostream>
#include <windows.h>
#include "Bypass.h"

int main() {
	std::cout << " Initializing Offsets...\n";
	Bypass::Init(); // Initialize Offsets & Cache Them
	std::cout << " Initializing Exploit and Loading Cheat Driver using PdFwKrnl...\n";
	Bypass::BypassStatus Status = Bypass::LoadCheatDriver("C:\\Driver.sys", "Driver Service Name", "C:\\Windows\\System32\\PdFwKrnl.sys", "Vuln Service Name"); // Load Cheat Driver & PdFwKrnl
	std::cout << " Status: " << Bypass::BypassStatusToString(Status) << std::endl;
	Sleep(5000);
	driver::unload("Driver Service Name"); // Unload Cheat Driver
	return 0;
}
