
<h1 align="center">
  <br>
  <img src=https://raw.githubusercontent.com/tlsbollei/NTDLL-Unhook/refs/heads/main/imgs/mnamom.png alt="Linux Peas" width="200"></a>
  <br>
  NTDLL-Unhook
  <br>
</h1>

<h4 align="center">A program written in C designed to remove security monitoring hooks from the NTDLL.dll <a href="http://electron.atom.io" target="_blank"></a></h4>

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](https://makeapullrequest.com)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)
[![Discord](https://img.shields.io/badge/Discord-7289DA?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/MqqPYJ2s)
## Introduction to NTDLL.dll
* NTDLL.dll (short for NT Layer DLL) is a critical system library in Windows. It acts as an intermediary between the Windows kernel (the core of the operating system) and user-mode applications. 
* It provides a wide array of low-level functions for processes and threads, memory management, system calls, exception handling, and more.
* Instead of bypassing the “infected” NTDLL.dll hooks by bypassing the dll completely (by performing a direct syscall), It is also possible to remove the EDR hook completely from the loaded module.
* This can be accomplished because of the following. The NTDLL.dll which is stored on disk isn’t hooked by itself. The ntdll on disk doesn’t contain the code of the EDR. This code is only injected when an application is started and the NTDLL.dll is loaded into the memory of that given process.
* There are quite a few ways to accomplish this. This C code focuses on unhooking the ntdll.dll by overwriting the hooked .txt section of the ntdll.dll and replacing it with the clean copy of the .text section of the ntdll.dll from disk.


![screenshot](https://raw.githubusercontent.com/tlsbollei/NTDLL-Unhook/refs/heads/main/imgs/ntdll.png)
### to better visualize the purpose of NTDLL.dll ^_^



## Key Features
* Uses ```GetCurrentProcess()``` to get a handle to the running process (the program itself)
* Retrieves the base address and size of the ```ntdll.dll``` module in memory using ```GetModuleInformation()```
* Opens the clean ```ntdll.dll``` file from the system directory ```(C:\Windows\System32\ntdll.dll)``` using ```CreateFileA()```
* Creates a file mapping with```CreateFileMapping()``` and maps the file into memory using ```MapViewOfFile()``` to access its contents
* Reads the DOS Header and NT Headers from the clean ```ntdll.dll``` in memory
* Locates the ```.text``` section by iterating over the section headers and finding the executable code
* Finds the base address of the loaded ```ntdll.dll``` in memory by using the information gathered earlier
* Identifies the ```.text section``` of the in-memory ```ntdll.dll```, where executable code is stored
* Uses ```VirtualProtect()``` to change the memory protection of the .text section to allow read, write, and execute operations, enabling modifications to the code
* Copies the ```.text``` section from the clean ```ntdll.dll``` (mapped from the disk) into the loaded ```ntdll.dll's``` .text section to replace any hooked or modified code
* After the replacement, the script restores the original memory protection of the ```.text``` section using ```VirtualProtect()```, setting it back to its previous state to prevent further modifications
* Closes handles related to the process, file, and memory mappings to free resources and prevent memory leaks using ```CloseHandle()```
* Unloads the ```ntdll.dll``` module from the process using ```FreeLibrary()``` to clean up after operations are complete




 [![forthebadge](https://forthebadge.com/images/featured/featured-oooo-kill-em.svg)](https://forthebadge.com)


## You may also like...
- [Linux Privilege Escalation](https://github.com/tlsbollei/peas) - A script written in bash - looks for potential privilege escalation vectors on a linux machine
- [SHA-256 Crack](https://github.com/tlsbollei/sha256crack) - SHA256 cracking tool written in C++ utilizing 2 attack modes - a Dictionary attack and a Brute Force attack with a customizable charset and max length


> GitHub [tlsbollei](https://github.com/tlsbollei) &nbsp;&middot;&nbsp;
> Instagram [0fa102](https://www.instagram.com/0fa102/)
> Telegram [boleii655](https://t.me/boleii655)
