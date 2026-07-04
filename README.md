# SSD Clone & GPT Partition Expansion Guide
> Cloning a 256GB SSD to 512GB using Balena Etcher, fixing a BSD boot error caused by GPT misalignment, and extending the partition via Diskpart.

---

## Overview

This guide documents how to:
1. Clone a 256GB SSD to a 512GB SSD using **Balena Etcher** while preserving all data
2. Fix a **Blue Screen of Death (BSD) boot error** caused by GPT partition misalignment after cloning
3. Use **Diskpart** (via external bootable drive) to **remap the GPT partition table** and restore boot
4. Use **Disk Management** to **extend the partition** and use the full 512GB of available space

> When cloning a GPT disk, the backup GPT header stays at the end of the *original* disk size. The cloned drive will trigger a **BSD boot error** and fail to start Windows until the partition table is remapped with Diskpart.

---

## The Problem

After cloning and swapping to the 512GB SSD, Windows fails to boot with a **Blue Screen of Death (BSD)**. This happens because:

- Balena Etcher copies the partition layout exactly as-is from the source disk
- GPT disks store a **backup partition table at the very end of the disk**
- On the 512GB drive, that backup table is now misplaced (still pointing to the 256GB boundary)
- Windows cannot find a valid boot partition

> All cloned drives are bootable. They just need the GPT partition table remapped after cloning. Once fixed, the drive boots normally.

Two separate tools are used for two different purposes:
- **Diskpart** remaps the GPT partition table so the drive can boot
- **Disk Management** extends the partition to use the full 512GB space

---

## Requirements

| Tool | Purpose |
|---|---|
| [Balena Etcher](https://etcher.balena.io/) | Disk cloning |
| USB enclosure / external drive caddy | Boot from the original 256GB SSD externally |
| 512GB SSD | Target drive (installed inside the laptop) |

---

## Step 1: Clone the SSD with Balena Etcher

1. Connect your **512GB SSD** via USB enclosure or second SATA port
2. Open **Balena Etcher**
3. Select **Clone drive**
4. Select your **256GB SSD** as source
5. Select your **512GB SSD** as target
6. Click **Flash** and wait for the process to complete

> All your data, OS, and files are now copied to the 512GB drive.
> The drive will only show 256GB usable. Do NOT skip Step 2.

---

## Step 2: Fix GPT Boot Error with Diskpart

The system will not boot. You will get a **BSD error**. Since the 512GB SSD is already installed inside the laptop and Windows cannot load from it, you need an external environment to run Diskpart and fix the GPT table.

There are two ways to get a working CMD environment:

---

### Method A: Boot from the original 256GB SSD externally

> No Windows ISO needed. The original cloned drive is a fully working OS. Just plug it in externally and boot from it.

**Setup:**
- **Inside the laptop** 512GB SSD (cloned, not booting, BSD error)
- **External USB enclosure** original 256GB SSD (working OS, used to boot)

**Steps:**
1. Connect your **256GB SSD** in a USB enclosure
2. Restart and enter the boot menu (`F11`, `F12`, or `DEL` depending on your machine)
3. Select the **external USB drive** as boot device
4. Windows boots normally from the 256GB external drive
5. Open **CMD as Administrator**

---

### Method B: Boot from a Windows USB installation drive

> Use this if you do not have a USB enclosure or prefer a clean recovery environment.

**Steps:**
1. Create a **bootable Windows USB drive** using the [Media Creation Tool](https://www.microsoft.com/software-download/windows11)
2. Restart and enter the boot menu (`F11`, `F12`, or `DEL` depending on your machine)
3. Select the **USB drive** as boot device
4. When the Windows setup screen appears, press `Shift + F10` to open **CMD directly**

> `Shift + F10` opens a command prompt from within the Windows setup environment without going through the full installation.

### Run Diskpart

```cmd
diskpart
```
```cmd
list disk
```

Identify your 512GB SSD (e.g., Disk 1)

```cmd
select disk 1
```
```cmd
list partition
```

> You will see the existing partitions cloned from the 256GB drive.

### Fix the GPT header

```cmd
recover
```

> This repairs the GPT backup header and moves it to the correct end of the 512GB disk. The drive will now be recognized properly and can boot.

```cmd
exit
```

### UEFI Boot Mode Required

GPT partition tables only work with **UEFI boot mode**. Before restarting:

1. Enter your **BIOS/UEFI settings** (press `DEL`, `F2`, or `F10` on startup)
2. Make sure **Boot Mode** is set to **UEFI** (not Legacy / CSM)
3. Disable **CSM (Compatibility Support Module)** if enabled
4. Save and exit

> If the system is set to Legacy/BIOS mode, it will fail to boot from a GPT disk even after the partition table is fixed.

Restart and boot normally from your new 512GB SSD.

---

## Step 3: Extend the Partition with Disk Management

> **Diskpart** was only used to **remap/fix the GPT table**. To extend the partition and use the remaining unallocated space, use **Disk Management** instead.

Once booted into Windows on your 512GB SSD:

1. Right-click the **Start Menu** > **Disk Management**
2. You will see your main partition with **unallocated space** next to it
3. Right-click your main partition > **Extend Volume**
4. Follow the wizard to use all remaining unallocated space
5. Click **Finish**

> Your partition now uses the full 512GB.

---

## Result

| | 256GB SSD (original) | 512GB SSD (clone) |
|---|---|---|
| Data | Preserved | Preserved |
| Bootable | Yes | Yes (after GPT remap) |
| Usable space | 256GB | 512GB (after partition extend) |
| Backup copy | Yes | Yes |

> Both drives are valid bootable backups. Any cloned GPT drive just needs to be remapped with Diskpart before it can boot.

---

## Key Takeaway

> **All cloned GPT drives are bootable. They just need to be remapped after cloning.**
>
> GPT disks store a backup partition table at the very end of the disk.
> When cloned to a larger drive, that backup table is misplaced, causing a BSD boot error.
> Boot Windows from the original drive connected externally, run `recover` in Diskpart
> to remap the GPT header on the new internal drive, then make sure
> **UEFI boot mode is enabled in BIOS** GPT partitions require UEFI to boot.
> No Windows ISO required.

---

## Author

**Dinaverse** [GitHub](https://github.com/Dinaverse) | [LinkedIn](https://www.linkedin.com/in/dinacima)
