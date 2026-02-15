# Linux vs Windows & Virtualization — Short Notes

## Windows Operating System
Developed by :contentReference[oaicite:0]{index=0}. Mostly used in personal and office computers.

**Features**
- GUI based and user-friendly
- Paid / licensed software
- Best for desktop applications
- Uses PowerShell & Command Prompt

---

## Linux Operating System
Open-source OS widely used in servers, cloud and DevOps.

**Features**
- Free and open-source
- Secure and stable
- Command-line oriented
- Used in servers/cloud
- Many distributions (Ubuntu, CentOS, RedHat)

---

## Linux vs Windows

| Feature | Windows | Linux |
|------|------|------|
| License | Paid | Free |
| Usage | Desktop | Server/Cloud |
| Security | Moderate | High |
| Customization | Limited | Highly customizable |
| CLI | CMD / PowerShell | Bash Terminal |
| DevOps | Less used | Preferred |

---

## Virtual Machine (VM)

**Definition:**  
A software computer running inside another computer.

Example: Run Linux inside Windows.

**Why used in DevOps**
- Test applications
- Simulate servers
- System isolation
- Practice Linux safely

### Key Terms
- **Hypervisor** – Creates VMs (:contentReference[oaicite:1]{index=1}, VirtualBox)
- **Host OS** – Main OS (Windows)
- **Guest OS** – OS inside VM (Linux)

### Network Modes
- **NAT** → Shares host internet
- **Bridged** → Gets separate IP

---

## WSL (Windows Subsystem for Linux)

Run Linux inside Windows without full VM.

**Features**
- Lightweight
- Faster than VM
- Direct Windows integration

### WSL vs VM

| Feature | WSL | VM |
|------|------|------|
| OS | Partial Linux | Full OS |
| Speed | Faster | Slower |
| Resource Usage | Low | High |
| Isolation | Less | More |
| Setup | Easy | Complex |

---

## VMware Installation (Summary)

Download from :contentReference[oaicite:2]{index=2} account → install → disable Hyper-V → enable virtualization in BIOS → install OS ISO → create VM.

---

## Ubuntu Server Setup (Quick Steps)
1. Create new VM
2. Attach ISO
3. Allocate RAM & CPU
4. Install OS
5. Create user
6. Enable SSH
7. Update system

```bash
sudo apt update && sudo apt upgrade

Basic Linux Commands
File Management
pwd        # current directory
ls         # list files
cd dir     # change directory
mkdir d    # create folder
rm file    # delete file
cp a b     # copy
mv a b     # move/rename

File Viewing
cat file
less file
head file
tail file
nano file
vim file

Search
grep "text" file
find / -name "*.txt"

System Info
uname -a
df -h
free -h
top
whoami

Networking
ip a
ping google.com

Packages (Ubuntu)
sudo apt update
sudo apt install nginx
sudo apt remove nginx

Important Concepts
vi Editor

i → insert

Esc → exit insert

:w → save

:q → quit

:wq → save & quit

LTS

Long-Term Support release (stable & supported ~5 years).

rm -rf

Force delete folder and all contents:

rm -rf folder_name

Wildcards

* → any characters

? → single character

[ ] → specific characters
