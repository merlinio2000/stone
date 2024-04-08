

# BIOS 

- old, 16-bit model
- relies on MBR
- many attacks


# UEFI

- no MBR, replaced with GPT (GUID partition table)
- Secure Boot - binaries are crypto signed (X.509) 
- legacy mode runs UEFI as if it was [[#BIOS]]
	- doesnt support Secure Boot
	- works with MBR

### EFI

UEFI uses a architecture independent VM, allows to execute
EFI (`.efi`) binaries

- EFI binaries are stored on the EFI System Partition (ESP)
	- FAT filesystem

#### EFI boot manager

selects which EFI binaries should be executed by the VM (e.g. bootloader)
Each OS must provide a EFI binary as its bootloader




