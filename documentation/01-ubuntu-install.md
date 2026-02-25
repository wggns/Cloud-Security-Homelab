For this project, I installed Ubuntu Server LTS (64-bit) on an HP EliteDesk Mini PC.

I chose Ubuntu Server instead of Ubuntu Desktop because:

It is lightweight (no GUI)

It runs primarily via CLI

It is better suited for logging, security testing, and server environments

It aligns with cybersecurity and cloud lab objectives

Ubuntu Server does not include a graphical interface by default.

1. Download Ubuntu Server ISO

Download:

Ubuntu Server LTS (64-bit)
From the official Ubuntu website. https://ubuntu.com/download

2. Create a Bootable USB Drive

After downloading the ISO file, you must create a bootable flash drive.

Requirements:

USB flash drive (8GB minimum)

I used a 64GB SanDisk USB

Software Used:

Rufus (on Windows) https://rufus.ie/en/

Rufus Configuration:

Device: Select your USB drive

Boot Selection: Select the Ubuntu Server ISO file

Partition Scheme: GPT

Target System: UEFI (non-CSM)

File System: FAT32

Click Start

Wait until Rufus displays DONE.

3. Boot from USB (HP EliteDesk Mini PC)

Insert the USB drive into the Mini PC

Power on the machine

Immediately press ESC repeatedly

When the Startup Menu appears, press F9 (Boot Device Options)

Select the USB drive

Press Enter

The system will now boot into the Ubuntu Server installer.

4. Ubuntu Server Installation Configuration

During installation, select the following options:

Language

English

Keyboard

English (US)

Network Configuration

If using Ethernet:

DHCP is automatically detected

No manual configuration required

If using WiFi:

Select your SSID

Enter the WiFi password

5. Storage Configuration

Select:

Use entire disk

Automatic partitioning

⚠️ Note:
This replaces the previous operating system (Windows) with Ubuntu Server.

6. Install OpenSSH Server

During installation, select:

✔ Install OpenSSH Server

This enables:

Remote management

SSH access from Kali Linux or management laptop

Secure administration of the server

This step is critical for a cybersecurity lab environment.

7. Final Installation Steps

After installation completes:

Remove the USB flash drive

Press Enter to reboot

The system will now boot from the internal SSD

You should see a CLI login screen similar to:

Ubuntu 22.04 LTS
login:

At this point, Ubuntu Server is successfully installed.
