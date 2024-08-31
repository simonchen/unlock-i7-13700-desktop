# unlock-i7-13700-desktop
Comprehensive guidance teaching you how to unlock TDP/POWER/AC-LOAD-LINE for Intel i7-13700 desktop CPU
(it may be able to apply similar methodolgy to any Intel 13/14th desktop CPU)

# Background
This guidance is for that your motherboard BIOS doesn't provide any options to unlock Temperature Limit, Power Limit (PL1/PL2), AC-Load line etc.
and your BIOS have no protection with UEFI variables .

# Prerequirests
You should prepare something as follows, either you can find them in here.

- Create a bootable USB disk
  Download modGRUBShell.efi from https://github.com/datasone/grub-mod-setup_var
  and rename it to BOOTX64.EFI
  Then, manually create a folder EFI in the USB drive, and continue to create a subfolder BOOT in the EFI folder,
  Put BOOTX64.EFI in EFI\BOOT\

- RU TOOL: http://ruexe.blogspot.com/
  Download RU.EFI and put it in EFI\BOOT\

- Intel BIOS dump tool - FPTW64.exe

# Dumps/Decodes "CPUSetup" section 
The steps that can refer to https://www.bios-mods.com/forum/showthread.php?tid=40039
Detailedly, you firstly dump orginal BIOS by FPTW64.exe, then load the bios file in UEFI Tool, 
then search for 'CPUSetup' section and save as a file (e.g, cpusetup_section.txt) , then utilizing ifrextractor.exe to extract/decode the file that you just saved as from UEFI Tool.

# Lookup UEFI variables for unlock option
Now, you open the decoded 'CPUSetup' section file in any text editor, search UEFI variables that you want to unlock (see below),
e.g, search "Tcc Offset Lock Enable", this will position to the line where you see 'VarOffset' value that's the actual register address you will need to change by RU tool (see below - **Unlock by RU tool**)
Below are options that you would like to change, each option that need to tweak one more UEFI variables (i.e, the actual register address represented in VarOffset)

- Temperature Limit
  ```
  "Tcc Offset Lock Enable", VarOffset: 0x1CD, Default value: 1 (Enable)
  "Bi-directional PROCHOT#", VarOffset: 0x7A, Default value: 1 (Enable)
  "Disable PROCHOT# Output", VarOffset: 0x7B, Default value: 1 (Enable)
  ```
  
- AC Load line
  ```
  "AC Loadline", VarOffset: 0x132, Default value: 0
  ```
  
# Unlock by RU tool
Booting the USB drive you made of (see Prerequirests), then type 'RU' command to launch it
press shortcut key "ALT + =" switching to 'CPUSetup' hex register editor, furthermore, you should press

CTRL+PgDn/PgUp : go to next / previous ranges of hex registers and move up/down/left/right arrow key to locate the actual register that you want to change

Once you changed the values of the register , then press CTRL + W to write it into registers.

When you finished all changes, you should press ALT + Q to quit RU tool, and type in "reset' command to restart PC.

