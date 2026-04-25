# Domain 101 — System Architecture

Notes for LPIC-101 (System Architecture), focusing on boot process and init systems.

---

## Boot Process (Correct Order)

**BIOS/UEFI → GRUB → Kernel → init/systemd**

This order is commonly tested.

### BIOS (legacy firmware)
- Legacy firmware (older systems)
- Typical Linux filesystems used in `/boot`: **ext2/ext3/ext4** (common in many setups)

### UEFI (modern firmware)
- Modern firmware
- Uses the **EFI System Partition (ESP)**, commonly mounted at:
  - `/boot/efi`
- Typical filesystem for ESP: **FAT32 (vfat)**

### GRUB (bootloader)
- Bootloader responsible for loading the Linux kernel.

Important files:
- `/etc/default/grub` → main configuration file you edit
- `/boot/grub/grub.cfg` → auto-generated configuration (**do not edit manually**)

Generate/rebuild `grub.cfg` (depends on distro):
- Debian/Ubuntu:
  - `sudo update-grub`
- Generic approach:
  - `sudo grub-mkconfig -o /boot/grub/grub.cfg`

### Kernel
- The core of the operating system.

---

## Init Systems

### systemd (modern init system)
- The most common modern init system.
- Runs as **PID 1**.

### SysVinit (legacy init system)
- Older init system (conceptual knowledge is useful for the exam).

---

## systemd Basics (Commands)

Start a service now:
```bash
sudo systemctl start <service>
```

Enable a service at boot:
```bash
sudo systemctl enable <service>
```

Switch to another target immediately:
```bash
sudo systemctl isolate <target>
```

Set the default target:
```bash
sudo systemctl set-default <target>
```

View the current default target:
```bash
systemctl get-default
```

List active units (what is running/loaded now):
```bash
systemctl list-units
```

List unit files installed on the system (what exists on disk):
```bash
systemctl list-unit-files
```

List targets (installed unit files of type target):
```bash
systemctl list-unit-files --type=target
```

---

Exam tip:

Show what is in use now
```bash
systemctl list-units
```

Shows what exists on the system.
```bash
systemctl list-unit-files
```



