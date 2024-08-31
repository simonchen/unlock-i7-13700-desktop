# unlock-i7-13700-desktop
Comprehensive guidance teaching you how to unlock TDP/POWER/AC-LOAD-LINE for Intel CPU i7-13700 desktop

# Background
This guidance is for that your motherboard BIOS doesn't provide any options to unlock Temperature Limit, Power Limit (PL1/PL2), AC-Load line etc.
and your BIOS have no protection with UEFI variables .

# Prerequirests
You should prepare these tools as follows, either you can find them in here.

- Create USB boot disk
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
Now, you open the decoded 'CPUSetup' section file in any text editor, search UEFI variables that have related to specific option  that you want to unlock (see below)

- Temperature Limit
  
  
