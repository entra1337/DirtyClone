# DirtyClone (CVE-2026-43503) - Python PoC

**Non-official Python port of DirtyClone** — a Linux kernel local privilege escalation vulnerability.

This repository contains a **working Proof of Concept** that allows an unprivileged local user to gain root privileges by exploiting page-cache corruption via cloned socket buffers.

---

## About DirtyClone

DirtyClone (CVE-2026-43503) is the fourth member of the **Dirty* family** (DirtyPipe → DirtyFrag → DirtyClone).

It abuses improper flag propagation in `__pskb_copy_fclone()` when using the TEE netfilter target with ESP-in-UDP. This allows an attacker to perform **in-place decryption** directly into file-backed page cache memory, even after previous DirtyFrag mitigations.

- **CVSS**: 8.8 (High)
- **Affected Kernels**: Roughly Linux 7.1-rc1 to rc4 (before commit `48f6a5356a33`)
- **Requirements**: Unprivileged user namespaces enabled (`user.max_user_namespaces > 0`)

**Credits**: Original research and technique by **JFrog Security Research**. This is an independent Python reimplementation.

---

## Features

- Pure Python implementation (no compilation needed)
- Overwrites `/etc/passwd` to add a new uid=0 user
- Spawns an interactive root shell
- Clean & well-commented code
- Works on most vulnerable distributions

---

Demo
<img src="https://github.com/user-attachments/assets/7a8ec634-62fb-4c6b-bab7-52495eb70e96" alt="Proof of Concept">

Disclaimer
This tool is for educational and security research purposes only.
Unauthorized use on systems you do not own is illegal.
Use responsibly.

References

JFrog Security Research - DirtyClone Writeup (link when available)
CVE-2026-43503
Linux kernel fix: 48f6a5356a33

## Usage

```bash
# 1. Clone the repo
git clone https://github.com/entra1337/DirtyClone.git
cd DirtyClone

# 2. Run the exploit
python3 dirtyclone.py


