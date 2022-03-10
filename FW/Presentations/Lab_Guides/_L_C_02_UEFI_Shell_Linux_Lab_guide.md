
## ## Slide  1   Platform Build Lab
<br><br><br><br><br>
##  UEFI & EDK II Training 

#### UEFI Shell Lab - Linux

<br>
<a href='http://www.tianocore.org'>tianocore.org</a>

<!---
 Lab_Guide.md for UEFI / EDK II Training  UEFI Shell Linux Lab

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
## Slide  2  Lesson Objective

###  Lesson Objective  <br>

- Run UEFI Shell  OVMF with QEMU
- Run UEFI Shell Commands 
- Run UEFI Shell Scripts 

  

---
## Slide  3  UEFI Shell Lab with Emulator Section

###  UEFI Shell Lab with Emulator 





## Slide  4  QEMU Running OVMF
 <b>QEMU Running OVMF</b> 

<br>
<br>
<br>
Open a terminal


Change to run-ovmf directory 
```
  bash$ cd $HOME/run-ovmf
```

Run the RunQemu.sh Linux shell script
```
bash$ . RunQemu.sh
```
See Platform Build lab for setup OVMF

---

## Slide  5  QEMU Running OVMF

###  QEMU Running OVMF

Type "F2" to get into the emulation setup or "Exit" from the Shell prompt 

---
## Slide  6  QEMU boot to UEFI Shell

###  QQEMU boot to UEFI Shell

---
## Slide  7  UEFI Shell Commands

### UEFI Shell Commands]

Commands from the Command Line Interface


---
## Slide  8  Common Shell Commands 
###  Common Shell Commands For Debugging 

```shell
help 
mm
mem
memmap
drivers
devices
devtree
dh
Load
dmpstore
pci
stall
```

- "-b" is the command line parameter for breaking after each page.


Note:

Next for this lab there are a few shell commands that will help us with debugging. For example if you are writing a driver, you would want to get familiar with these shell commands. Each of these commands will have a help option to give you further information about these commands.

We are not going to go all were these in detail but just to make you aware of the shell commands.


---

## Slide  9  Shell Help Command 
###  Shell Help 


<span style="background-color: #000000"><font color="#FFFF00">&nbsp;
<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
help -b</font>&nbsp; </font></span>



```
Shell> help -b
acpiview      - Display ACPI Table information.
alias         - Displays, creates, or deletes UEFI Shell aliases.
attrib        - Displays or modifies the attributes of files or directories.
bcfg          - Manages the boot and driver options that are stored in NVRAM.
cd            - Displays or changes the current directory.
cls           - Clears the console output and optionally changes the background and foreground color.
comp          - Compares the contents of two files on a byte-for-byte basis.
connect       - Binds a driver to a specific device and starts the driver.
cp            - Copies one or more files or directories to another location.
date          - Displays and sets the current date for the system.
dblk          - Displays one or more blocks from a block device.
devices       - Displays the list of devices managed by UEFI drivers.
devtree       - Displays the UEFI Driver Model compliant device tree.
dh            - Displays the device handles in the UEFI environment.
disconnect    - Disconnects one or more drivers from the specified devices.
dmem          - Displays the contents of system or device memory.
dmpstore      - Manages all UEFI variables.
drivers       - Displays the UEFI driver list.
drvcfg        - Invokes the driver configuration.
drvdiag       - Invokes the Driver Diagnostics Protocol.
echo          - Controls script file command echoing or displays a message.
edit          - Provides a full screen text editor for ASCII or UCS-2 files.
eficompress   - Compresses a file using UEFI Compression Algorithm.
Press Enter to continue or 'Q' to break:
```
Note:

Next let’s just try the help shell command. So once you reach the shell go ahead and type: "help –b"
And what you will see is the list of all the shell commands built into this platform followed by a one liner information about each command.
To exit, this emulation simply type: "reset"


---
## Slide  10  Shell memmap Command 
###  Shell "memmap" 

<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
 memmap</font>&nbsp;&nbsp; </font></span>


Displays the memory map maintained by the UEFI environment
```
Shell> memmap
. . .

BS_Data    00000117FC9E7000-00000117FC9F3FFF 000000000000000D 000000000000000F
RT_Data    00000117FC9F4000-00000117FC9F4FFF 0000000000000001 800000000000000F
BS_Data    00000117FC9F5000-00000117FCA1CFFF 0000000000000028 000000000000000F
RT_Data    00000117FCA1D000-00000117FCA1FFFF 0000000000000003 800000000000000F
MMIO       00000117F4A00000-00000117F4A0BFFF 000000000000000C 8000000000000001
 
  Reserved  :              0 Pages (0 Bytes)
  LoaderCode:            309 Pages (1,265,664 Bytes)
  LoaderData:              0 Pages (0 Bytes)
  BS_Code   :          1,256 Pages (5,144,576 Bytes)
  BS_Data   :          5,983 Pages (24,506,368 Bytes)
  RT_Code   :             98 Pages (401,408 Bytes)
  RT_Data   :            193 Pages (790,528 Bytes)
  ACPI_Recl :              0 Pages (0 Bytes)
  ACPI_NVS  :              0 Pages (0 Bytes)
  MMIO      :             12 Pages (49,152 Bytes)
  MMIO_Port :              0 Pages (0 Bytes)
  PalCode   :              0 Pages (0 Bytes)
  Available :         24,929 Pages (102,109,184 Bytes)
  Persistent:              0 Pages (0 Bytes)
              -------------- 
Total Memory:            128 MB (134,217,728 Bytes)
Shell> 
```

---

## Slide  11  Shell mm Command help 
###  Shell "mm" 

<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
 mm -? -b</font>&nbsp;&nbsp; </font></span>

Help for "mm" command shows options for different types of memory and I/O that can be modified
```
Shell> mm -? -b
Displays or modifies MEM/MMIO/IO/PCI/PCIE address space.
 
MM Address [Value] [-w 1|2|4|8] [-MEM | -MMIO | -IO | -PCI | -PCIE] [-n]
 
  Address - Starting address in hexadecimal format.
  Value   - The value to write in hexadecimal format.
  -MEM    - Memory Address type
  -MMIO   - Memory Mapped IO Address type
  -IO     - IO Address type
  -PCI    - PCI Configuration Space Address type:
            Address format: ssssbbddffrr
              ssss - Segment
              bb   - Bus
              dd   - Device
              ff   - Function
              rr   - Register
  -PCIE   - PCIE Configuration Space Address type:
            Address format: ssssbbddffrrr
              ssss - Segment
              bb   - Bus
              dd   - Device
              ff   - Function
              rrr  - Register
  -w      - Unit size accessed in bytes:
              1    - 1 byte
              2    - 2 bytes
              4    - 4 bytes
              8    - 8 bytes
  -n      - Non-interactive mode
 
NOTES:
  1.  If the address type parameter is not specified, address type defaults
      to the 'MEM' type.
  2.  If the 'Value' parameter is specified, the '-n' option is used and
      the command writes the value to the
      specified address in non-interactive mode. If the 'Value' parameter is
      not specified, only the current contents in the address are displayed.
  3.  If the '-w' option is not specified, unit size defaults to 1 byte.
  4.  If the PCI address type is specified, the 'Address' parameter must
      follow the PCI Configuration Space Address format above. The 'PCI'
      command can be used to determine the address for a specified device.
      It is listed in the PCI configuration space dump information in the
      following format: "[EFI ssbbddffxx]".
  5.  If the PCIE address type is specified, the 'Address' parameter must
      follow the PCIE Configuration Space Address format above.
  6.  In interactive mode, type a hex value to modify, 'q' or '.' to exit.
      If the '-n' option is specified, it runs in non-interactive mode,
      which supports batch file operation without user intervention.
  7.  Not all PCI configuration register locations are writable.
  8.  MM will only write the specified value. Read-modify-write operations
      are not supported.
  9.  The 'Address' parameter must be aligned on a boundary of the
      specified width.
  10. Not all addresses are safe to access. Access to any improper address
      can bring unexpected results.
 
EXAMPLES:
  * To display or modify memory:
    Address 0x1b07288, default width=1 byte:
    fs0:\> mm 1b07288
    MEM  0x0000000001B07288 : 0x6D >
    MEM  0x0000000001B07289 : 0x6D >
    MEM  0x0000000001B0728A : 0x61 > 80
    MEM  0x0000000001B0728B : 0x70 > q
    fs0:\> mm 1b07288
    MEM  0x0000000001B07288 : 0x6D >
    MEM  0x0000000001B07289 : 0x6D >
    MEM  0x0000000001B0728A : 0x80 >        *Modified
    MEM  0x0000000001B0728B : 0x70 > q
 
  * To modify memory: Address 0x1b07288, width = 2 bytes:
    Shell> mm 1b07288 -w 2
    MEM  0x0000000001B07288 : 0x6D6D >
    MEM  0x0000000001B0728A : 0x7061 > 55aa
    MEM  0x0000000001B0728C : 0x358C > q
    Shell> mm 1b07288 -w 2
    MEM  0x0000000001B07288 : 0x6D6D >
    MEM  0x0000000001B0728A : 0x55AA >      *Modified
    MEM  0x0000000001B0728C : 0x358C > q
 
  * To display IO space:   Address 80h, width = 4 bytes:
    Shell> mm 80 -w 4 -IO
    IO  0x0000000000000080 : 0x000000FE >
    IO  0x0000000000000084 : 0x00FF5E6D > q
 
  * To modify IO space using non-interactive mode:
    Shell> mm 80 52 -w 1 -IO
    Shell> mm 80 -w 1 -IO
    IO  0x0000000000000080 : 0x52 > FE      *Modified
    IO  0x0000000000000081 : 0xFF >
    IO  0x0000000000000082 : 0x00 >
    IO  0x0000000000000083 : 0x00 >
    IO  0x0000000000000084 : 0x6D >
    IO  0x0000000000000085 : 0x5E >
    IO  0x0000000000000086 : 0xFF >
    IO  0x0000000000000087 : 0x00 > q
 
  * To display PCI configuration space, ss=0000, bb=00, dd=00, ff=00, rr=00:
    Shell> mm 000000000000 -PCI
    PCI  0x0000000000000000 : 0x86 >
    PCI  0x0000000000000001 : 0x80 >
    PCI  0x0000000000000002 : 0x30 >
    PCI  0x0000000000000003 : 0x11 >
    PCI  0x0000000000000004 : 0x06 >
    PCI  0x0000000000000005 : 0x00 > q
    These contents can also be displayed by 'PCI 00 00 00'.
 
  * To display PCIE configuration space, ss=0000, bb=06, dd=00, ff=00, rrr=000:
    Shell> mm 0000060000000 -PCIE
    PCIE  0x0000000060000000 : 0xAB >
    PCIE  0x0000000060000001 : 0x11 >
    PCIE  0x0000000060000002 : 0x61 >
    PCIE  0x0000000060000003 : 0x43 >
Shell>
```




---
## Slide  12  Shell mm   Command 
###  Shell "mm" 

<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
 mm 117FC9F5000 
 </font>&nbsp;&nbsp; </font></span>


**Pick a location from the MemMap command on Previous slides
<font color="#FFFFff"><span style="background-color: #000000"><br>
&nbsp;&nbsp;<font face="Consolas"> BS_Data    00000117FC9F5000-00000117FCA1CFFF 0000000000000028 000000000000000F</font> &nbsp;&nbsp; </span></font>

MM in can display / modify any location 


```
Shell> mm 117FC9F5000 
MEM 0x00000117FC9F5000 : 0x70 >

MEM 0x00000117FC9F5001 : 0x68 >

MEM 0x00000117FC9F5002 : 0x64 >

MEM 0x00000117FC9F5003 : 0x30 >

MEM 0x00000117FC9F5004 : 0x00 >?

Shell>
```


Try

<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
 mm 0 
 </font>&nbsp;&nbsp; </font></span>

Use "q" to quit

Note:

Press the "enter" key and the contents of each location is shown.

This command allows changing the contents of each memory location.


---
## Slide  13  Shell mem Command 
###  Shell "mem" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
mem
 </font>&nbsp;&nbsp; </font></span>

Displays the contents of the system or device memory
without arguments, displays the system memory configuration and
the UEFI System Table Pointer 
```
Shell> mem
Memory Address 00000117F8908018 78 Bytes
  F8908018: 49 42 49 20 53 59 53 54-46 00 02 00 78 00 00 00  *IBI SYSTF...x...*
  F8908028: 80 7B 1C A5 00 00 00 00-98 4D 9F FC 17 01 00 00  *.{.......M......*
  F8908038: 00 00 01 00 00 00 00 00-98 4C 83 FC 17 01 00 00  *.........L......*
  F8908048: B0 F1 3F 71 00 00 00 00-98 75 4C FC 17 01 00 00  *..?q.....uL.....*
  F8908058: 18 6F 4C FC 17 01 00 00-18 2F 7D FC 17 01 00 00  *.oL....../}.....*
  F8908068: 20 F5 3F 71 00 00 00 00-98 8B 90 F8 17 01 00 00  * .?q............*
  F8908078: A0 E5 B9 71 00 00 00 00-0A 00 00 00 00 00 00 00  *...q............*
  F8908088: 98 8C 90 F8 17 01 00 00-                         *........*

Valid EFI Header at Address 00000117F8908018
---------------------------------------------
System: Table Structure size 00000078 revision 00020046
ConIn (00000000713FF1B0) ConOut (00000117FC4C6F18) StdErr (00000000713FF520)
Runtime Services 00000117F8908B98
Boot Services    0000000071B9E5A0
SAL System Table 0000000000000000
ACPI Table       0000000000000000
ACPI 2.0 Table   0000000000000000
MPS Table        0000000000000000
SMBIOS Table     00000117FCA1E000
Shell>
```

Note:



---


## Slide  14  Shell drivers Command 
###  Shell "drivers" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
drivers -b
 </font>&nbsp;&nbsp; </font></span>

Displays the UEFI driver list.
```
Shell> drivers -b
            T   D
D           Y C I
R           P F A
V  VERSION  E G G #D #C DRIVER NAME                         IMAGE NAME
== ======== = = = == == =================================== ==========
47 0000000A D - -  2  - Platform Console Management Driver  ConPlatformDxe
48 0000000A D - -  2  - Platform Console Management Driver  ConPlatformDxe
49 0000000A B - -  2  2 Console Splitter Driver             ConSplitterDxe
4A 0000000A B - -  2  2 Console Splitter Driver             ConSplitterDxe
4B 0000000A ? - -  -  - Console Splitter Driver             ConSplitterDxe
4C 0000000A B - -  2  2 Console Splitter Driver             ConSplitterDxe
4D 0000000A ? - -  -  - Console Splitter Driver             ConSplitterDxe
51 0000000A D - -  2  - Graphics Console Driver             GraphicsConsoleDxe
52 0000000A B - -  1  1 Serial Terminal Driver              TerminalDxe
53 0000000A D - -  1  - Generic Disk I/O Driver             DiskIoDxe
54 0000000B ? - -  -  - Partition Driver(MBR/GPT/El Torito) PartitionDxe
57 0000000A ? - -  -  - PCI Bus Driver                      PciBusDxe
59 0000000A ? - -  -  - SCSI Bus Driver                     ScsiBus
5A 0000000A ? - -  -  - Scsi Disk Driver                    ScsiDisk
5B 0000000A B - -  1  5 Emu Bus Driver                      EmuBusDriver
5C 0000000A D - -  2  - Emulator GOP Driver                 EmuGopDxe
5D 0000000A D - -  1  - Emu Simple File System Driver       EmuSimpleFileSystem
5E 0000000A D - X  1  - Emu Block I/O Driver                EmuBlockIo
5F 0000000A D - -  1  - Emu SNP Driver                      EmuSnpDxe
60 0000000A ? - -  -  - VLAN Configuration Driver           VlanConfigDxe
61 0000000A ? - -  -  - MNP Network Service Driver          MnpDxe
62 0000000A ? - -  -  - ARP Network Service Driver          ArpDxe
63 0000000A ? - -  -  - DHCP Protocol Driver                Dhcp4Dxe
64 0000000A ? - -  -  - IP4 Network Service Driver          Ip4Dxe
65 0000000A ? - -  -  - UDP Network Service Driver          Udp4Dxe
66 0000000A ? - -  -  - MTFTP4 Network Service              Mtftp4Dxe
67 0000000A ? - -  -  - TCP Network Service Driver          TcpDxe
68 0000000A ? - -  -  - TCP Network Service Driver          TcpDxe
69 0000000A ? - -  -  - UEFI PXE Base Code Driver           UefiPxeBcDxe
6A 0000000A ? - -  -  - UEFI PXE Base Code Driver           UefiPxeBcDxe
6B 0000000A ? - -  -  - FAT File System Driver              Fat
Shell>
```

To get the description of each section use:  <span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
drivers -?
 </font>&nbsp;&nbsp; </font></span>





---
## Slide  15  Shell devices Command 
###  Shell "devices" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
devices
 </font>&nbsp;&nbsp; </font></span>

Displays a list of devices that UEFI drivers manage.

```
Shell> devices
     T   D
     Y C I
     P F A
CTRL E G G #P #D #C  Device Name
==== = = = == == === =========================================================
  1C R - -  0  1   5 VenHw(5CF32E0B-8EDF-2E44-9CDA-93205E99EC1C,00000000)
  20 R - -  0  1   1 VenHw(D3987D4B-971A-435F-8CAF-4967EB627241)/Uart(115200,8,N,1)
  4E D - -  2  0   0 Primary Console Input Device
  4F D - -  2  0   0 Primary Console Output Device
  6F B - -  1  7   2 GOP Window 1
  70 B - -  1  7   2 GOP Window 2
  71 D - -  1  1   0 .
  72 D - X  1  2   0 disk.dmg:FW
  73 D - -  1  1   0 VenHw(5CF32E0B-8EDF-2E44-9CDA-93205E99EC1C,00000000)/VenHw(FD5FBE54-8C35-B345-8A0F-7AC8A5FD0521,00000000)
  74 D - -  1  0   0 VT-100 Serial Console
Shell>

```



---
## Slide  16  Shell devtree Command 
###  Shell "devtree" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
devtree
 </font>&nbsp;&nbsp; </font></span>

Displays tree of devices currently managed by UEFI drivers.
```
Shell> devtree
 Ctrl[03] Fv(6D99E806-3D38-42C2-A095-5F4300BFD7DC)
 Ctrl[04] MemoryMapped(0xB,0x117F4A00000,0x117F4A1FFFF)
 Ctrl[13] MemoryMapped(0xB,0x117F4480000,0x117F49FFFFF)
 Ctrl[1C] VenHw(5CF32E0B-8EDF-2E44-9CDA-93205E99EC1C,00000000)
   Ctrl[6F] GOP Window 1
     Ctrl[4E] Primary Console Input Device
     Ctrl[4F] Primary Console Output Device
   Ctrl[70] GOP Window 2
     Ctrl[4E] Primary Console Input Device
     Ctrl[4F] Primary Console Output Device
   Ctrl[71] .
   Ctrl[72] disk.dmg:FW
   Ctrl[73] VenHw(5CF32E0B-8EDF-2E44-9CDA-93205E99EC1C,00000000)/VenHw(FD5FBE54-8C35-B345-8A0F-7AC8A5FD0521,00000000)
 Ctrl[20] VenHw(D3987D4B-971A-435F-8CAF-4967EB627241)/Uart(115200,8,N,1)
   Ctrl[74] VT-100 Serial Console
 Ctrl[2A] Fv(6D99E806-3D38-42C2-A095-5F4300BFD7DC)/FvFile(462CAA21-7614-4503-836E-8AB6F4662331)/Enter Setup
 Ctrl[2B] Fv(6D99E806-3D38-42C2-A095-5F4300BFD7DC)/FvFile(EEC25BDC-67F2-4D95-B1D5-F81B2039D11D)/BootManagerMenuApp
 Ctrl[2C] Fv(6D99E806-3D38-42C2-A095-5F4300BFD7DC)/FvFile(7C04A583-9E3E-4F1C-AD65-E05268D0B4D1)/Shell
 Ctrl[6D] VenHw(A04A27F4-DF00-4D42-B552-39511302113D)
 Ctrl[6E] VenHw(B3F56470-6141-4621-8F19-704E577AA9E8)
Shell>
```



---
## Slide  17  Shell handle Database Command 
###  Shell handle database - "dh" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
dh -b
 </font>&nbsp;&nbsp; </font></span>

Dump Handle - Displays the device handles associated with UEFI drivers


Also try "dh -d" with handle number to get more information on that handle.

```
Shell> dh -b
Handle dump
01: LoadedImage(DxeCore) 
02: Decompress 
03: FirmwareVolume2 DevicePath(..3D38-42C2-A095-5F4300BFD7DC)) FirmwareVolumeBlock 
04: DevicePath(..0x1A3F5300000,0x1A3F531FFFF)) FirmwareVolumeBlock 
05: FC1BCDB0-7D31-49AA-936A-A4600D9DD083 EE4E5898-3914-4259-9D6E-DC7BD79403CF 
06: ImageDevicePath(..87AB-47F9-A3FE-D50B76D89541)) LoadedImage(PcdDxe) 
07: GetPcdInfo GetPcdInfoProtocol Pcd Pcd 
08: ImageDevicePath(..A563-4561-B858-D8476F9DEFC4)) LoadedImage(Metronome) 
09: MetronomeArch 
0A: ImageDevicePath(..A7EB-4730-8C8E-CC466A9ECC3C)) LoadedImage(ReportStatusCodeRouterRuntimeDxe) 
0B: SmartCardReader RscHandler 
0C: ImageDevicePath(..8985-11DB-8429-0040D02B1835)) LoadedImage(RealTimeClock) 
0D: RealTimeClockArch 
0E: ImageDevicePath(..37AD-8743-BCF2-DF1A8FF12FAB)) LoadedImage(EmuReset) 
0F: ResetArch 
10: ImageDevicePath(..43B7-4784-95B1-F4226CB40CEE)) LoadedImage(RuntimeDxe) 
11: RuntimeArch 
12: ImageDevicePath(..96E8-2A4C-95F4-85248F989753)) LoadedImage(FwBlockService) 
13: FirmwareVolume2 DevicePath(..0x1A3F4D80000,0x1A3F52FFFFF)) FirmwareVolumeBlock 
Press ENTER to continue or 'Q' break:
```

---

## Slide  18  Shell Load Command 
###  Shell "load" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
load -?
 </font>&nbsp;&nbsp; </font></span>

Loads a UEFI driver into memory

```
Shell> load ?
Loads a UEFI driver into memory.
 
LOAD [-nc] file [file...]
 
  -nc  - Loads the driver, but does not connect the driver.
  File - Specifies a file that contains the image of the UEFI driver (wildcards are
         permitted).
 
NOTES:
  1. This command loads a driver into memory. It can load multiple files at
     one time. The file name supports wildcards.
  2. If the -nc flag is not specified, this command attempts to connect the
     driver to a proper device. It might also cause previously loaded drivers
     to be connected to their corresponding devices.
  3. Use the 'UNLOAD' command to unload a driver.
 
EXAMPLES:
  * To load a driver:
    fs0:\> load Isabus.efi
 
  * To load multiple drivers:
    fs0:\> load Isabus.efi IsaSerial.efi
 
  * To load multiple drivers using file name wildcards:
    fs0:\> load Isa*.efi
 
  * To load a driver without connecting it to a device:
    fs0:\> load -nc IsaBus.efi
Shell>
```

---
## Slide  19  Shell Load Command 
###  Shell "Dmpstore" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
dmpstore -all -b
 </font>&nbsp;&nbsp; </font></span>

Display the contents of the NVRAM variables
```
Shell> dmpstore -all -b
Variable NV+RT+BS 'EB704011-1402-11D3-8E77-00A0C969723B:MTC' DataSize = 0x04
  00000000: 03 00 00 00                                      *....*
Variable NV+RT+BS 'EFIGlobalVariable:BootOrder' DataSize = 0x0C
  00000000: 05 00 01 00 02 00 03 00-04 00 00 00              *............*
Variable NV+RT+BS 'EFIGlobalVariable:Boot0005' DataSize = 0x68
  00000000: 01 00 00 00 3C 00 55 00-45 00 46 00 49 00 20 00  *....<.U.E.F.I. .*
  00000010: 53 00 68 00 65 00 6C 00-6C 00 00 00 04 07 14 00  *S.h.e.l.l.......*
  00000020: 06 E8 99 6D 38 3D C2 42-A0 95 5F 43 00 BF D7 DC  *...m8=.B.._C....*
  00000030: 04 06 14 00 83 A5 04 7C-3E 9E 1C 4F AD 65 E0 52  *.......|>..O.e.R*
  00000040: 68 D0 B4 D1 04 04 10 00-53 00 68 00 65 00 6C 00  *h.......S.h.e.l.*
  00000050: 6C 00 00 00 7F FF 04 00-4E AC 08 81 11 9F 59 4D  *l.......N.....YM*
  00000060: 85 0E E2 1A 52 2C 59 B2-                         *....R,Y.*
Variable NV+RT+BS 'EFIGlobalVariable:Boot0004' DataSize = 0x9C
  00000000: 01 00 00 00 56 00 55 00-45 00 46 00 49 00 20 00  *....V.U.E.F.I. .*
  00000010: 42 00 6F 00 6F 00 74 00-4D 00 61 00 6E 00 61 00  *B.o.o.t.M.a.n.a.*
  00000020: 67 00 65 00 72 00 4D 00-65 00 6E 00 75 00 41 00  *g.e.r.M.e.n.u.A.*
  00000030: 70 00 70 00 00 00 04 07-14 00 06 E8 99 6D 38 3D  *p.p..........m8=*
  00000040: C2 42 A0 95 5F 43 00 BF-D7 DC 04 06 14 00 DC 5B  *.B.._C.........[*
  00000050: C2 EE F2 67 95 4D B1 D5-F8 1B 20 39 D1 1D 04 04  *...g.M.... 9....*
  00000060: 2A 00 42 00 6F 00 6F 00-74 00 4D 00 61 00 6E 00  **.B.o.o.t.M.a.n.*
  00000070: 61 00 67 00 65 00 72 00-4D 00 65 00 6E 00 75 00  *a.g.e.r.M.e.n.u.*
  00000080: 41 00 70 00 70 00 00 00-7F FF 04 00 4E AC 08 81  *A.p.p.......N...*
  00000090: 11 9F 59 4D 85 0E E2 1A-52 2C 59 B2              *..YM....R,Y.*
  Press ENTER to continue or 'Q' break:
```
---
## Slide  20  Shell Stall Command 
###  Shell "PCI" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
pci -? -b
 </font>&nbsp;&nbsp; </font></span>

Display the help for the PCI command
```
Displays PCI device list or PCI function configuration space and PCIe extended
configuration space.
 
PCI [Bus Dev [Func] [-s Seg] [-i [-ec ID]]]
 
  -s   - Specifies optional segment number (hexadecimal number).
  -i   - Displays interpreted information.
  -ec  - Displays detailed interpretation of specified PCIe extended capability
         ID (hexadecimal number).
  Bus  - Specifies a bus number (hexadecimal number).
  Dev  - Specifies a device number (hexadecimal number).
  Func - Specifies a function number (hexadecimal number).
 
NOTES:
  1. This command displays a list of all the PCI devices found in the system. It
     also displays the configuration space of a PCI device according to the
     specified bus (Bus), device (Dev), and function (Func) addresses. If the
     function address is not specified, it defaults to 0.
  2. The -i option displays verbose information for the specified PCI
     device. The PCI configuration space for the device is displayed with
     a detailed interpretation.
  3. If no parameters are specified, all PCI devices are listed.
  4. If the 'Bus' and 'Dev' parameters are specified but the 'Func' or
     'Seg' parameters are not, Function or Seg are set to the default value of 0.
 
EXAMPLES:
  * To display all PCI devices in the system:
    Shell> pci
 
  * To display the configuration space of Bus 0, Device 0, Function 0:
    Shell> pci 00 00 00 -i
 
  * To display configuration space of Segment 0, Bus 0, Device 0, Function 0:
    Shell> pci 00 00 00 -s 0

```
---
## Slide  21  Shell Stall Command 
###  Shell "stall" 
<span style="background-color: #000000"><font color="#FFFF00">&nbsp;&nbsp;<font face="Consolas">Shell&gt;</font></font><font color="#FFFFFF"><font face="Consolas"> 
stall 10000000
 </font>&nbsp;&nbsp; </font></span>

Stalls the operation for a specified number of microseconds

```
Shell> stall 10000000
Shell>
```

---




## Slide  22  UEFI Shell Lab Scripts Section


### UEFI Shell Scripts


Use Scripting with UEFI Shell 

---
## Slide  23  UEFI Shell Scripts 
###  UEFI Shell Scripts 
<br>
The UEFI Shell can execute commands from a file, which is called a batch script file (<font face="consolas" color="cyan"><b>.nsh</b></font> files).  
<br>
<br>
<font color="blue"><b>Benefits:</b></font> These files allow users to simplify routine or repetitive tasks. <br>

- Perform basic flow control.  
- Allow branching and looping in a script.  
- Allow users to control input and output and call other batch programs (known as script nesting).  

---

## Slide  24  Writing UEFI Shell Scripts
###  Writing UEFI Shell Scripts  



With the UEFI shell There is an editor included. This is a very simple editor but can help if running on the target system without an OS "Nice" editor available.

Shell editor help  menu - Cnt W

At the shell prompt
```
Shell> fs0:
FS0:\> edit HelloScript.nsh 
```

**Type:** `echo Hello World`  inside the editor  


- Press "F2" or "Control S" to save file
- Enter 
- Press "F3" or "Control-Q" to exit

---
## Slide  25  Hello World Script
###  Hello World Script 




In the shell, type HelloScript for the following result:

```
FS0:\> HelloScript.nsh
FS0:\> echo Hellow World
Hello World
FS0:\>
```

Close the QEMU



## Slide  26  UEFI Shell Nested Scripts 
###  UEFI Shell Nested Scripts  

QEMU: Copy the Scripts from the `~/FW/LabSampleCode/ShellScripts` to the run-ovmf directory  `~/run-ovmf/hda-contents`




---
## Slide  27  UEFI Shell Script Example
<br>
### UEFI Shell Script Example 

<font color="blue">Script1.nsh</font> 
```shell
# Simple UEFI Shell script file
echo  -off
script2.nsh
if exist %cwd%Mytime.log then
     type Mytime.log
endif
echo "%HThank you." "%VByeBye:) %N"
```
<font color="blue">Script2.nsh</font> 
```shell
# Show nested scripts
time > Mytime.log
for %a run (3 1 -1)
    echo %a counting down
endfor
```

Note:
walk through the script calling the second script
- if
- for loop
  - %a counting down...
  
---
## Slide  28  Run UEFI Shell Scripts 
###  Run UEFI Shell Scripts 

Run the RunQemu.sh from the terminal (Cnt-Alt-T)
```
   bash$ cd ~run-ovmf
    bash$ . RunQemu.sh
```


 At the Shell prompt Type  
```
Shell> fs0:
FS0:\> Script1

FS0:\> Edit Script1.nsh
```


--- 

## Slide  29  Run UEFI Shell Scripts cont 
###  Run UEFI Shell Scripts 

- Remove the "`#`" on the first line



- Press "F2" or "Control S" to save file
- Enter 
- Press "F3" or "Control-Q" to exit
- Type : `FS0:\> Script1`



---
## Slide 30  UEFI Shell Global Variables

### Use BCFG and Dmpstore



---
## Slide 31  Show the UEFI Boot Variables

At the Shell Prompt:
```
Shell> FS0:
Shell> BCFG Boot Dump
```
Note see the list of Boot000X options printed to the console

---
## Slide 32  Use the Dmpstore to Show the Boot Order

At the Shell Prompt:

```
FS0: > Dmpstore BootOrder
```
---
## Slide 33  Use the BCFG to Move a boot item 

Use BCFG to Move the 4th boot item too 1st location.

Then verify using the `dmpstore`

(Hint: use `BCFG -? -b` for help menu)

The dmpstore output should look like:

```
Variable NV+RT+BS 'EFIGlobalVariable:BootOrder' DataSize = 0x0C
  00000000: 00 00 01 00 02 00-03 00 04 00              *..........*
```

Solution:
```
bcfg boot mv 04 00
```

---
## Slide 34  Use the BCFG to Add a boot item  

Copy the old EFI Shell from  
~/src/edk2-ws/edk2/ShellPkg/OldShell/Shell_FullX64.efi to the run-ovmf directory  ~/run-ovmf/hda-contents

```
bash$ cp ~/src/edk2-ws/edk2/ShellPkg/OldShell/Shell_FullX64.efi  ~/run-ovmf/hda-contents
```

Use BCFG to Add  a 06 entry for a new boot option with  `Shell_FullX64.efi`

Then verify using the `BCFG Boot Dump`

Hint: make sure Shell_FullX64.efi is in the FS0: directory by doing: 
```
FS0:> Dir 
```
After the bcfg add, The output should look like
```
. . .
Option: 04. Variable: Boot0004   
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
## Slide  35  Summary

### Summary  <br>

- Run UEFI Shell  in QEMU
- Run UEFI Shell Commands 
- Run UEFI Shell Scripts 

 

---
## Slide  36  Questions
### Questions

---
## Slide  37  Return to Main Training Page
### Return to Main Training Page



---
## Slide  38  Logo Slide

### logo

Return to Training Table of contents for next presentation <a href="https://github.com/tianocore-training/Tianocore_Training_Contents/wiki">link</a>

---
## Slide  39  Acknowledgements
#### Acknowledgements 

```
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

Copyright (c) 2021, Intel Corporation. All rights reserved.
**/

```
