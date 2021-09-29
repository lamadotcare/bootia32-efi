# bootia32-efi
EFI boot blob and build scripts for devices using IA32 UEFI

# Help, I've fallen into UEFI and I can't get out!

I made this because, perhaps like you, I was trying to install Linux on an older x86_64-based tablet and found myself unable to boot and dropping into UEFI..

# Devices supported
Pretty much anything using Intel [Silvermont](https://en.wikipedia.org/wiki/Silvermont) -based "[Bay Trail](https://www.intel.com/content/www/us/en/products/platforms/details/bay-trail.html)" CPUs:
- Intel Atom® Processor E3800 and Z3700 Series
- Intel® Pentium® and Celeron® Processor N- and J-Series.

### Known to work:
- Acer NP15A
- Multilaser M8W tablet
- Asus T100
- Lenovo Tab2

---
# How-Tos
## Create a bootable USB stick from a Lubuntu ISO
I tested several Ubuntu distributions with these chips and found Lubuntu to be the most performant and lightweight on resources.  For the tests I booted each in "live CD" mode, so none of the systems had access to swap

With Lubuntu I could simultaneously open all the default sponsored tabs in Firefox (Facebook, Reddit, other heavy sites), run LibreOffice Write and Calc, load a 4k image into GIMP, and have a YouTube video running full screen in just under 1.5GB RAM.  The other Ubuntu distros OOM'd and died long before I could get to YouTube.

1. Fetch the Lubuntu ISO from https://lubuntu.me/downloads/
2. Get a copy of bootia32.efi either by downloading it from this repo or building it yourself.
3. Back up any valuable files from your USB stick because they'll be deleted in the next step.
4. Create a new GPT partition table on the USB stick with Gnome Disks, parted, Windows Disk Manager, or any other partition management utility that supports GPT.
5. Create a new FAT32 partition and format it.
6. Mount the ISO so you can access the files within it.  Windows 10 and most Linux distributions can do this without additional software.
7. Make "hidden" files visible on the ISO.  Hidden files begin with a single '.' character.  Windows Explorer and Gnome Files both have this capability in their view menus. 
8. **Copy** all files from the ISO onto your USB stick's FAT32 partition.
9. Ignore any errors about unsupported symlinks.  Those symlinks are not required for a successful installation.
10. **Copy** the bootia32.efi file into /EFI/boot on your USB stick.  You should see other .efi files in there already.
11. Unmount the USB stick and boot from it.

# Building from sources
Read the contents of bootstrap.sh and build.sh (in this repo) and follow the steps or just run the scripts.

# Due credit
I relied on these sources to help me figure out this issue:
- https://wiki.debian.org/UEFI#Support_for_mixed-mode_systems:_64-bit_system_with_32-bit_UEFI
- https://sturmflut.github.io/linux/ubuntu/2015/02/04/installing-ubuntu-on-baytrail-tablets-version-2/
- https://github.com/hirotakaster/baytail-bootia32.efi
- In particular I used the build instructions from John Wells's repo: https://github.com/jfwells/linux-asus-t100ta
- https://unix.stackexchange.com/questions/257363/create-a-uefi-bootable-usb-stick-from-an-iso-image-with-gparted
- https://askubuntu.com/questions/395879/how-to-create-uefi-only-bootable-usb-live-media
