---
title: Cracking PDF Password with Hashcat - A Step-by-Step Guide
published: 2025-04-25
updated: 2025-04-25
description: 'A detailed tutorial on using Hashcat to crack password-protected PDF files on Kali Linux'
image: '/assets/img/posts/2025-04-25-Cracking-PDF-Password-with-Hashcat/hashcat-progress.jpg'
tags: [Hashcat, PDF, Security, Password, Pentesting, Linux]
category: 'Tutorial'
draft: false
---

## Introduction

This comprehensive guide will teach you how to crack a password-protected PDF file using **Hashcat** on **Kali Linux**. Hashcat is a powerful password recovery tool that can crack various types of hashes, including those used to secure PDF files. 

### ⚠️ Legal Disclaimer

This guide is for **educational purposes only** and is intended for:
- Security professionals conducting authorized penetration testing
- System administrators recovering access to legitimate files
- Security researchers studying password protection mechanisms

**DO NOT** use this knowledge for:
- Unauthorized access to protected documents
- Breaking into systems or networks
- Any illegal activities

Always obtain proper authorization before attempting to crack passwords. Unauthorized password cracking may violate local and international laws.

## What You Need

### 1. System Requirements

#### Hardware Requirements
- CPU: Multi-core processor (more cores = faster cracking)
- GPU: NVIDIA or AMD GPU for hardware acceleration (optional but recommended)
- RAM: Minimum 8GB (16GB or more recommended)
- Storage: 20GB free space for wordlists

#### Software Requirements

1. **Kali Linux**
   - Latest version recommended
   - Can be run from USB, VM, or native installation
   - Other Linux distributions work too, but commands may vary

2. **Hashcat**
   - Pre-installed on Kali Linux
   - Installation if needed: `sudo apt update && sudo apt install hashcat`
   - Version 6.0.0 or higher recommended
   - Check installation: `hashcat --version`

3. **Required Tools**
   - John the Ripper (for pdf2john): `sudo apt install john`
   - Python 3.x: Pre-installed on Kali
   - Text editor (nano/vim)

### 2. Files Needed

1. **Password-Protected PDF File**
   - Supported versions: PDF 1.1 - 1.7
   - File size: Preferably under 100MB
   - Must be readable (not corrupted)

2. **Wordlist**
   - Default: `rockyou.txt` (/usr/share/wordlists/rockyou.txt)
   - Download if missing: 
     ```bash
     sudo gunzip /usr/share/wordlists/rockyou.txt.gz
     ```
   - Other wordlists:
     - SecLists: `sudo apt install seclists`
     - Custom wordlists based on target

### 3. Optional Tools

1. **GPU Drivers**
   - NVIDIA: `sudo apt install nvidia-driver`
   - AMD: `sudo apt install mesa-opencl-icd`

2. **Monitoring Tools**
   - htop: `sudo apt install htop`
   - nvtop (for NVIDIA GPUs): `sudo apt install nvtop`

## Step 1: Extract the Hash from the PDF

Before using Hashcat, you need to extract the hash from the PDF file. The hash is a cryptographic representation of the password protection mechanism used in the PDF. There are several methods to extract this hash.

### Understanding PDF Password Protection

PDF files can be protected with two types of passwords:

1. **User Password (Document Open Password)**
   - Prevents opening the document
   - Required for basic file access
   - What we'll be cracking in this guide

2. **Owner Password (Permissions Password)**
   - Controls document permissions
   - Restricts printing, copying, editing
   - More complex to crack

### Option 1: Using `pdf2john` (Recommended Method)

`pdf2john` is the most reliable tool for hash extraction. It's specifically designed to handle various PDF encryption methods.

#### Installation

```bash
# Install John the Ripper if not already installed
sudo apt update
sudo apt install john
```

#### Hash Extraction Steps

1. **Prepare Your Environment**
   ```bash
   # Create a working directory
   mkdir pdf_crack
   cd pdf_crack
   ```

2. **Copy Your PDF**
   ```bash
   # Replace /path/to/your.pdf with actual path
   cp /path/to/your.pdf ./protected.pdf
   ```

3. **Extract the Hash**
   ```bash
   pdf2john protected.pdf > hash.txt
   ```
   - Replace `protected.pdf` with your PDF filename
   - The `>` operator redirects output to hash.txt

4. **Verify the Hash**
   ```bash
   cat hash.txt
   ```

![Hash Output](/assets/img/posts/2025-04-25-Cracking-PDF-Password-with-Hashcat/pdf-hashcat-extract.jpg)

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ cat hash.txt
protected.pdf:$pdf$2*3*128*-4*1*16*d05276a71ab81c45a6a3bd0363be0606*32*8424c2551c7d03e964f00e04ffc8637428bf4e5e4e758a4164004e56fffa0108*32*38d28f6967ed3a8602824da3d47449ceae970293fd62ee126fafd0e7a28438a2

┌──(kali㉿kali)-[~/Desktop]
└─$ 
```

#### Understanding the Output

The hash output will look something like this:
```
protected.pdf:$pdf$4*4*128*fr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rd...*1*16*fr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rdfr0stb1rd
```

Let's break down the components:
- `$pdf$`: Format identifier
- `4`: PDF version
- `128`: Key length
- Rest: Encryption data

> Remove `protected.pdf:` from the output to get the hash only.
{: .prompt-danger }

Your hash.txt file should look like the following:

`$pdf$2*3*128*-4*1*16*d05276a71ab81c45a6a3bd0363be0606*32*8424c2551c7d03e964f00e04ffc8637428bf4e5e4e758a4164004e56fffa0108*32*38d28f6967ed3a8602824da3d47449ceae970293fd62ee126fafd0e7a28438a2`

### Option 2: Using a Python Script (Alternative)

If `pdf2john` doesn't work, you can try the Python script `pdf2Hashcat.py` as an alternative. **Be cautious** when running this script as it may not be as reliable as `pdf2john`. Search for `pdf2Hashcat.py` online and download the script

## Step 2: Identify the Hash Type

Hashcat requires you to specify the correct hash type for successful password recovery. PDF files use different hash types based on their version and security settings.

### PDF Version and Hash Type Mapping

| PDF Version | Acrobat Version | Hash Type | Security Features |
|-------------|----------------|-----------|-------------------|
| 1.1 - 1.3 | Acrobat 2 - 4 | `10500` | Basic RC4 encryption |
| 1.4 - 1.6 | Acrobat 5 - 8 | `10600` | Enhanced RC4/AES |
| 1.7 Level 3 | Acrobat 9 | `10700` | AES-128 |
| 1.7 Level 8 | Acrobat 10 - 11 | `10400` | AES-256 |

### How to Check PDF Version

1. **Using exiftool**:
   ```bash
   # Install exiftool
   sudo apt install exiftool

   # Check PDF version
   exiftool protected.pdf | grep "PDF Version"
   ```

2. **Using pdfinfo**:
   ```bash
   # Install poppler-utils
   sudo apt install poppler-utils

   # Check PDF version
   pdfinfo protected.pdf | grep "PDF version"
   ```

3. **Manual Check**:
   - Open PDF in text editor
   - Look for `%PDF-X.X` at the start

![PDF Version Check](/assets/img/posts/2025-04-25-Cracking-PDF-Password-with-Hashcat/pdf-version-check.jpg)

```bash
┌──(kali㉿kali)-[~/Desktop/pdf_crack]
└─$ exiftool protected.pdf | grep "PDF Version"
PDF Version                     : 1.7
                                                                                                                     
┌──(kali㉿kali)-[~/Desktop/pdf_crack]
└─$ 
```

## Step 3: Running Hashcat

### Hardware Optimization

1. **GPU Setup** (Recommended)
   ```bash
   # Check GPU support
   hashcat -I

   # Enable GPU monitoring
   watch -n 1 nvidia-smi  # For NVIDIA
   watch -n 1 radeontop   # For AMD
   ```

2. **CPU Optimization**
   ```bash
   # Set performance mode
   sudo cpupower frequency-set -g performance

   # Monitor CPU usage
   htop
   ```

### Attack Modes

1. **Wordlist Attack** (Mode 0)
   ```bash
   hashcat -m <hash_type> -a 0 hash.txt wordlist.txt
   ```

2. **Combination Attack** (Mode 1)
   ```bash
   # Combine two wordlists
   hashcat -m <hash_type> -a 1 hash.txt list1.txt list2.txt
   ```

3. **Mask Attack** (Mode 3)
   ```bash
   # Pattern-based attack
   hashcat -m <hash_type> -a 3 hash.txt ?d?d?d?d?d?d  # 6 digits
   ```

4. **Hybrid Attack** (Mode 6)
   ```bash
   # Wordlist + Mask
   hashcat -m <hash_type> -a 6 hash.txt wordlist.txt ?d?d?d
   ```

### Advanced Options

```bash
# Basic command with options
hashcat -m <hash_type> -a 0 hash.txt wordlist.txt \
   --status            \ # Show progress
   --status-timer 10   \ # Update every 10 seconds
   -w 3                \ # Workload profile (1-4)
   --force             \ # Ignore warnings
   -O                  \ # Optimize for 32 chars or less
   --session mysession \ # Save session
   -r rules/best64.rule  # Apply rules
```

### Performance Tuning

1. **Workload Profiles**
   - `-w 1`: Low impact on system
   - `-w 2`: Default balance
   - `-w 3`: High performance
   - `-w 4`: Maximum performance

2. **Kernel Optimization**
   ```bash
   # For better GPU performance
   hashcat --kernel-accel 1 --kernel-loops 1
   ```

3. **Memory Management**
   ```bash
   # Segment size adjustment
   hashcat --segment-size 512
   ```

### Monitoring Progress

1. **Status Screen**
   - Speed: H/s (Hashes per second)
   - Progress: % complete
   - Time Remaining: ETA
   - Recovered: Found passwords

2. **Save Progress**
   ```bash
   # Save session
   hashcat ... --session mysession

   # Restore session
   hashcat --session mysession --restore
   ```

3. **Output Options**
   ```bash
   # Save cracked passwords
   hashcat ... --outfile cracked.txt

   # Show cracked only
   hashcat ... --show
   ```

### Start Cracking

```bash
hashcat -m 10500 hash.txt wordlist.txt
```

After running the command, you will see the progress of the cracking process. Be patient, it may take a while.

```bash
┌──(kali㉿kali)-[~/Desktop/pdf_crack]
└─$ hashcat -m 10500 hash.txt wordlist.txt
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
============================================================================================================================================
* Device #1: cpu-sandybridge-16th Gen Intel(R) Core(TM) i9-12900KF @ 8.20GHz, 21593/50244 MB (21590 MB allocatable), 32MCU

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

Watchdog: Temperature abort trigger set to 90c

Host memory required for this attack: 2 MB

Dictionary cache built:
* Filename..: wordlist.txt
* Passwords.: 50
* Bytes.....: 506
* Keyspace..: 50
* Runtime...: 0 secs

The wordlist or mask that you are using is too small.
This means that hashcat cannot use the full parallel power of your device(s).
Unless you supply more work, your cracking speed will drop.
For tips on supplying more work, see: https://hashcat.net/faq/morework

Approaching final keyspace - workload adjusted.           

$pdf$2*3*128*-4*1*16*d05276a71ab81c45a6a3bd0363be0606*32*8424c2551c7d03e964f00e04ffc8637428bf4e5e4e758a4164004e56fffa0108*32*38d28f6967ed3a8602824da3d47449ceae970293fd62ee126fafd0e7a28438a2:fr0stb1rd
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 10500 (PDF 1.4 - 1.6 (Acrobat 5 - 8))
Hash.Target......: $pdf$2*3*128*-4*1*16*d05276a71ab81c45a6a3bd0363be06...8438a2
Time.Started.....: Sun May  4 08:59:40 2025 (0 secs)
Time.Estimated...: Sun May  4 08:59:40 2025 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (wordlist.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:      158 H/s (0.30ms) @ Accel:256 Loops:70 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 50/50 (100.00%)
Rejected.........: 0/50 (0.00%)
Restore.Point....: 0/50 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-70
Candidate.Engine.: Device Generator
Candidates.#1....: hunter2 -> hypernova
Hardware.Mon.#1..: Util: 12%

Started: Sun May  4 08:59:17 2025
Stopped: Sun May  4 08:59:41 2025
                                                                                                                     
┌──(kali㉿kali)-[~/Desktop/pdf_crack]
└─$ 
```

If the password is cracked successfully it will give you the hash along with the password, as shown below:

```bash
$pdf$2*3*128*-4*1*16*d05276a71ab81c45a6a3bd0363be0606*32*8424c2551c7d03e964f00e04ffc8637428bf4e5e4e758a4164004e56fffa0108*32*38d28f6967ed3a8602824da3d47449ceae970293fd62ee126fafd0e7a28438a2:fr0stb1rd
```

The password is: **fr0stb1rd**

### Pot File

Hashcat writes all cracked hashes to a pot file. The pot file is a text file that contains the cracked hash and the password.

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ cat ~/.local/share/hashcat/hashcat.potfile
$pdf$4*4*128*-4*1*16*489810bcd5953bf4871f6ee95308f7c6*32*021eacdfc91fb1d57e46fb8c0ea50c9b28bf4e5e4e758a4164004e56fffa0108*32*9a79d589019a7d332527723a4df175c6b3c192574569fc487c3437c25ea5024f:istanbulTURKEY
$pdf$2*3*128*-4*1*16*d05276a71ab81c45a6a3bd0363be0606*32*8424c2551c7d03e964f00e04ffc8637428bf4e5e4e758a4164004e56fffa0108*32*38d28f6967ed3a8602824da3d47449ceae970293fd62ee126fafd0e7a28438a2:fr0stb1rd

┌──(kali㉿kali)-[~/Desktop]
└─$ 
```

You can find the pot file in `~/.local/share/hashcat/hashcat.potfile`.

## Conclusion

Successful PDF password recovery with Hashcat requires:
- Correct hash type identification
- Appropriate attack strategy
- Optimized hardware usage
- Patience and persistence

Remember: This knowledge should only be used for legitimate password recovery scenarios.

![Hashcat Progress](/assets/img/posts/2025-04-25-Cracking-PDF-Password-with-Hashcat/hashcat-progress.jpg)

> **Resource Usage**: Monitor system resources carefully. Password cracking can be intensive on hardware.

> **Time Estimation**: Success rate varies greatly based on password complexity and hardware capabilities.

> **Note**: Hashcat is a powerful tool, but it should be used responsibly. Unauthorized password cracking may be illegal.
