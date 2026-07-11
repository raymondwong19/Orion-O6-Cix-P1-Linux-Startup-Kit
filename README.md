Just a pre-setup bootloader and Linux kernel for Cix P1 (ACPI/UEFI) and I had a Orion O6 - but it isn't board specific since the firmware will handle the DT.
Originally it was just Armbian's UEFI-arm64 - I replaced the rootfs with Rocky Linux - partition requirements is listed below.
Mali GPU works with Panthor - but yeah - the snooping is one way only - leading to a CPU cache flush bottleneck that makes it nigh useless.


As it is a active devboard at the moment - you shouldn't really connect it to the Internet - as it doesn't really get security updates - for the features don't work - forget security. It's testing only.


7.0.0-37-cix-MODULES.7z == Modules - put it inside your /lib/modules

boot.tar.gz == The Boot Directory - overwrite everything in your /boot with this

EFI.tar.gz == Files for the ESP System Partition - it is a separate partition from the /boot dir which shall sit on your ext4 linux partition.


Partition Label Requirements :


Linux Partition : LABEL="armbi_root" UUID="9edba17a-c2c0-42f3-b1c4-bd49f8fd54e6" TYPE="ext4" PARTLABEL="rootfs" PARTUUID="c16eb8e1-8d1c-4bc2-a537-fd20e671076d"

ESP System Partition : LABEL_FATBOOT="ARMBI_EFI" LABEL="ARMBI_EFI" UUID="98A6-7555" TYPE="vfat" PARTLABEL="efi" PARTUUID="cb7211b6-f31c-4aea-a7f2-0179c8603aa1"


ESP System Partition shall be 256MB in size - but then again, as long as it fits it doesn't matter. Linux Partition can be any size - it doesn't matter all once again - as long as it fits.
Partition numbers or order matters not either - only the labels matter because the GRUB configuration never used anything else - and there is no rootfs - set it up yourself in the Linux Partition.
