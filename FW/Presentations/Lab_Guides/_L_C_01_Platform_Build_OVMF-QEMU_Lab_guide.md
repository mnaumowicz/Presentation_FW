## Slide 1  Platform Build Lab  - OVMF Lab

## UEFI & EDK II Training

 Platform Build Lab  - OVMF

<br>
<a href='http://www.tianocore.org'>tianocore.org</a>


<!---
 Lab_Guide.md for Platform Build Ovmf Linux Lab

  Copyright (c) 2020-2021, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->


---  
## Slide 2  Platform Build Labs

### Platform Build Labs 
<br>
   

- Build a EDK II Platform using OVMF package
- Run Ovmf using Qemu



---
## Slide 3  Lab 1 -BUILD OVMFPKG Section


### Build  OVMFPKG

 Setup OvmfPkg to build and run w/ QEMU

---
## Slide 4  Pre-requisites Ubuntu 16.04  


### Pre-requisites Ubuntu 16.04 

Instructions from: tianocore wiki Ubuntu_1610 
- Example Ubuntu 16.04

The following need to be accessible for building Edk2, From the terminal prompt (Cnt-Alt-T):
```
bash$ sudo apt-get install build-essential uuid-dev iasl git gcc-5 nasm python3-distutils-extra


build-essential - Informational list of build-essential packages
uuid-dev - Universally Unique ID library (headers and static libraries)
iasl - Intel ASL compiler/decompiler (also provided by acpica-tools)
git - support for git revision control system
gcc-5 - GNU C compiler (v5.4.0 as of Ubuntu 16.04 LTS)
nasm - General-purpose x86 assembler 
python3 - distutils - extra - distutils module from the Python standard library


bash$ sudo apt-get install qemu
```

Qemu – Emulation with Intel architecture with UEFI Shell 


---
## Slide 5  Pre-requisites Clear Linux* Project 


### Pre-requisites Clear Linux* Project
- Example Using Clear Linux* Project 

The following need to be accessible for building Edk2, From the terminal prompt (Cnt-Alt-T):
```
bash$  sudo swupd bundle-add devpkg-util-linux
```

Devpkg-util-linux – includes bundles for developer tools for writing  "C" Applications included:
 gcc, nasm, uuid, etc.

```
bash$  sudo swupd bundle-add kvm-host
```

Qemu – Emulation with Intel architecture with UEFI Shell 



---
## Slide 6   Create QEMU Run Script


### Create QEMU Run Script
Create a run-ovmf directory under the home directory
```
bash$ cd ~
bash$ mkdir run-ovmf
bash$ cd run-ovmf
```

Create a directory to use as a hard disk image
```
bash$ mkdir hda-contents
```

Create a Linux shell script to run the QEMU from the run-ovmf directory
```
bash$ gedit RunQemu.sh
```
Type in the following for the file RunQemu.sh
```
qemu-system-x86_64 -pflash bios.bin -hda fat:rw:hda-contents -net none -debugcon file:debug.log -global isa-debugcon.iobase=0x402
```
Save and Exit


---
## Slide 7  Download the EDK II Source Code 

### Download the EDK II Source Code

Open a terminal prompt and create a source working directory
```
bash$ mkdir ~/src 
bash$ cd ~/src
bash$ mkdir edk2-ws 
bash$ cd edk2-ws 
```

Note:  if behind a firewall, set PROXYS FIRST
```
bash$ export http_proxy=http://proxy-us.company.com:911
bash$ export ftp_proxy=$http_proxy
```

Download edk2 source tree using Git

```
bash$ git clone -b Edk2Lab_22Q1 https://github.com/tianocore-training/edk2.git
bash$ git clone https://github.com/tianocore/edk2-libc.git

```

Download the Submodules and Checkout the Lab Branch
```
bash$  cd edk2
bash$  git submodule update --init
bash$  cd ..
```
---
## Slide 8  Setup Lab Material 
### Setup Lab Material

---
## Slide 9  Download Lab_Material_FW  
### Download Lab Material<br>
Download the Lab_Material_FW.zip from :  <a href="https://github.com/tianocore-training/Lab_Material_FW/archive/refs/heads/main.zip">github.com Lab_Matrial_FW.zip</a><br>
<br>
OR<br>
Use `git clone` to download the Lab_Material_FW<span>
```bash
bash$ cd $HOME
bash$ git clone https://github.com/tianocore-training/Lab_Material_FW.git
```
Directory Lab_Material_FW will be created

```
   FW 
    - Documentation 
	- DriverWizard 
	- edk2-ws      
	- edk2Linux 
	- LabSampleCode 
	- Nasm
	
```



---
## Slide 10  Build  Edk2 -getting the Source 
<b>Build EDK II OVMF </b><br>

– Extract the Source  

Extract the Downloaded `Lab_Material_FW-main.zip to $HOME `


Note:
Extract the Downloaded Lab_Material_FW.zip to $HOME (this will create a directory `~/FW` )

---
## Slide 11  Build  Edk2 -getting the Source 02
<b>Build EDK II  </b><br>
 - Copy edk2-ws 


From the downloaded Lab_Material_FW folder,<br> <b>copy</b> and <b>paste</b> folder `"../edk2-ws"` to `"~src"`


<i>Note:</i> Overwrite existing files and directories

---
## Slide 12  BUILD EDK II OVMF - Building BaseTool
]
<b>BUILD EDK II OVMF - Building BaseTools</b><br>
 
 Export work space & platform path
 
``` 
bash$ cd ~/src/edk2-ws
bash$ export WORKSPACE=$PWD
bash$ export PACKAGES_PATH=$WORKSPACE/edk2:$WORKSPACE/edk2-libc
```
 
 Run Make
 
``` 
bash$ cd edk2
bash$ make –C BaseTools/
```



Make sure the tests pass OK


---
## Slide 13  Build Ovmf Platform
<b>Build Ovmf Platform </b><br>
 



---

## Slide 14  BUILD EDK II OVMF -Update Target.txt
<br>


### BUILD EDK II OVMF -Update Target.txt

#### What is OVMF?
Open Virtual Machine Firmware - Build with edk2



Open Terminal prompt & Cd to work space directory 
```
bash$ cd ~/src/edk2-ws/edk2
bash$ . edksetup.sh

```

 - Edit / Update `conf/Target.txt`
``` 
bash$ gedit Conf/target.txt
```
Update the following define statements
```
    ACTIVE_PLATFORM       = OvmfPkg/OvmfPkgX64.dsc
	
    TARGET_ARCH           = X64
	. . .
    TOOL_CHAIN_TAG        = GCC5
```

### Save and Exit

### Build OvmfPkg
```
$> build -D ADD_SHELL_STRING -a X64
```


---
## Slide 15  Build Edk2 -build inside Prompt
<b>Build EDK II  OVMF</b><br>
- Inside Terminal



Finished build
---

## Slide 16  BUILD EDK II OVMF -Verify Build Succeeded

### BUILD EDK II OVMF -Verify Build Succeeded

OVMF.fd should be in the Build directory

For GCC5 with X64, it should be located at
```  
   ~/src/edk2-ws/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd
```

---
## Slide 17  Invoke QEMU
<br>

### Invoke QEMU
Change to run-ovmf directory under the home directory
```
bash$ cd $HOME/run-ovmf
```
Copy the `OVMF.fd` BIOS image created from the build to the run-ovmf directory naming it `bios.bin`
```
bash$ cp ~/src/edk2-ws/Build/OvmfX64/DEBUG_GCC5/FV/OVMF.fd bios.bin
```
Run the RunQemu.sh Linux shell script
```
bash$ . RunQemu.sh
```

QEMU will open to the UEFI SHell prompt



---
## Slide 18  Show the UEFI Boot Variables

At the Shell Prompt:
```
Shell> FS0:
Shell> BCFG Boot Dump
```
Note see the list of Boot000X options printed to the console

---
## Slide 19  Use the Dmpstore to Show the Boot Order

At the Shell Prompt:

```
FS0: > Dmpstore BootOrder
```
---
## Slide 20  Use the BCFG to Move a boot item 

Use BCFG to Move the 4th boot item too 1st location.

Then verify using the `dmpstore`

(Hint: use `BCFG -? -b` for help menu)

The dmpstore output should look like:

```
Variable NV+RT+BS 'EFIGlobalVariable:BootOrder' DataSize = 0x0C
  00000000: 00 00 01 00 02 00 03 00              *.....*
```

Solution:
```
bcfg boot mv 03 00
```

---
## Slide 21  Use the BCFG to Add a boot item  

Copy the old EFI Shell from  
~/src/edk2-ws/ShellPkg/OldShell/Shell_FullX64.efi to the run-ovmf directory  ~/run-ovmf/hda-contents

```
bash$ cp ~/src/edk2-ws/ShellPkg/OldShell/Shell_FullX64.efi  ~/run-ovmf/hda-contents
```

Use BCFG to Add  a 04 entry for a new boot option with  `Shell_FullX64.efi`

Then verify using the `BCFG Boot Dump`

Hint: make sure Shell_FullX64.efi is in the FS0: directory by doing: 
```
FS0:> Dir 
```
After the bcfg add, The output should look like
```
. . .
Option: 04. Variable: Boot0006   
  Desc    - Old EFI Shell 1.0
  DevPath - VenHw(5CF32E0B-8EDF-2E44-9CDA-93205E99EC1C,00000000)/VenHw(964E5B22-6459-11D2-8E39-00A0C969723B,00000000)/\Shell_FullX64.efi
  Optional- N
```

To exit, Close QEMU

Solution:
```
bcfg boot add 04 Shell_fullX64.efi "Old EFI Shell 1.0"
```



---  
## Slide 22  Summary
### Summary <br>

- 
- Build a EDK II Platform using OVMF package
- Run Ovmf using Qemu

---
## Slide 23  Questions
<br>
Questions

---
## Slide 24  return to main
<b>Return to Main Training Page</b>
<br>
<br>
<br>
<br>
<br>
Return to Training Table of contents for next presentation <a href="https://github.com/tianocore-training/Tianocore_Training_Contents/wiki#schedule--outline">link</a>



---
## Slide 25  Logo Slide
<br><br><br>



---
## Slide 26  Acknowledgements
#### Acknowledgements

```c++
/**
Redistribution and use in source (original document form) and 'compiled' forms (converted
to PDF, epub, HTML and other formats) with or without modification, are permitted provided
that the following conditions are met:

Redistributions of source code (original document form) must retain the above copyright 
notice, this list of conditions and the following disclaimer as the first lines of this 
file unmodified.

Redistributions in compiled form (transformed to other DTDs, converted to PDF, epub, HTML
and other formats) must reproduce the above copyright notice, this list of conditions and 
the following disclaimer in the documentation and/or other materials provided with the 
distribution.

THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR IMPLIED 
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND 
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL TIANOCORE PROJECT BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES 
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, 
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF ADVISED OF THE POSSIBILITY 
OF SUCH DAMAGE.

Copyright (c) 2020, Intel Corporation. All rights reserved.
**/

```

