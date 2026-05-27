# -Assembly-Language-Setup-using-WSL-NASM-in-Windows-

This repository contains Assembly Language programs and setup instructions for running NASM on Windows using WSL (Windows Subsystem for Linux).

---

# What is WSL?

WSL (Windows Subsystem for Linux) allows you to run Linux directly inside Windows without using a virtual machine.

With WSL, you can:
- Use Linux commands
- Run NASM assembler
- Compile Assembly programs
- Use Git and GitHub easily

---

# Requirements

- Windows 10/11
- Internet connection
- Administrator access

---

# Step 1: Install WSL

Open **PowerShell as Administrator** and run:

```powershell
wsl --install
```

---

# Step 2: Install Ubuntu

1. Open Microsoft Store
2. Search for **Ubuntu**
3. Install Ubuntu (Recommended: Ubuntu 22.04 LTS)

Launch Ubuntu and create:
- Username
- Password

---

# Step 3: Update Ubuntu

Open Ubuntu terminal and run:

```bash
sudo apt update
sudo apt upgrade -y
```

---

# Step 4: Install NASM

Install NASM assembler:

```bash
sudo apt install nasm -y
```

Check version:

```bash
nasm -v
```
Example output:

```text
NASM version 2.x.x
```

---



# Step 5: Create Working Directory

```bash
mkdir foldername
cd flodername
```

---

# Step 6: Create First Assembly Program

Create file:

```bash
nano hello.asm
```
# Step 6: Write Assembly Program Code

Example 32 bit :
```asm
section .data
    msg db "Hello from 32-bit Assembly!", 10
    len equ $ - msg

section .text
    global _start

_start:
    mov eax, 4
    mov ebx, 1
    mov ecx, msg
    mov edx, len
    int 0x80

    mov eax, 1
    xor ebx, ebx
    int 0x80
```
Example 64 bit :
``` asm
section .data
    msg db "Hello from 64-bit Assembly!", 10
    len equ $ - msg

section .text
    global _start

_start:
    mov rax, 1
    mov rdi, 1
    mov rsi, msg
    mov rdx, len
    syscall

    mov rax, 60
    xor rdi, rdi
    syscall
```

Save:
- CTRL + O
- Enter
- CTRL + X

---

Step 6: To run the code
```bash for 32bit
nasm -f elf32 -o hello.o hello.asm
ld -o hello hello.o
./hello 
```
```bash for 64bit
nasm -f elf64 -o hello.o hello.asm
ld -o hello hello.o
./hello 
```
