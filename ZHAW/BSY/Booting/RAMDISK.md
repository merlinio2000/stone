
To load the OS it needs to access hard drives and filesystems but the software to access the disk is stored on the disk :)


Solution:
# Initial RAM disk image (initrd)

- stored in the same area as the kernel
- gets decompressed into ram by bootloader
- contains Kernel modules + device-special files (/dev/null, /dev/stdin,...)




