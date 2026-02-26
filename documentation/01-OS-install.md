Ubuntu Server Installation (HP EliteDesk Mini PC)
1. Project Context

For this lab environment, Ubuntu Server 22.04 LTS (64-bit) was installed on an HP EliteDesk Mini PC.

Ubuntu Server was selected instead of Ubuntu Desktop for the following reasons:

Lightweight (no graphical user interface)

CLI-focused environment

Better suited for logging and security testing

Aligns with cybersecurity and cloud lab objectives

Reduced attack surface compared to GUI-based systems

Ubuntu Server does not include a graphical interface by default, making it ideal for infrastructure and monitoring roles.

2. Download Ubuntu Server ISO

Download the official ISO:

Ubuntu Server LTS (64-bit)
https://ubuntu.com/download

Always download directly from the official Ubuntu website to ensure integrity.

3. Create a Bootable USB Drive
Requirements

USB flash drive (minimum 8GB)

64GB SanDisk USB used for this installation

Rufus (Windows utility)

Download Rufus:
https://rufus.ie/en/

Rufus Configuration

Use the following configuration:

Device: Select USB drive

Boot Selection: Ubuntu Server ISO

Partition Scheme: GPT

Target System: UEFI (non-CSM)

File System: FAT32

Click Start.

Wait until Rufus displays DONE before removing the USB drive.

4. Boot from USB (HP EliteDesk Mini PC)

Insert USB drive into Mini PC

Power on the machine

Immediately press ESC repeatedly

When the Startup Menu appears, press F9 (Boot Device Options)

Select the USB drive

Press Enter

The system will boot into the Ubuntu Server installer.

5. Ubuntu Server Installation Configuration
Language

English

Keyboard

English (US)

Network Configuration

If using Ethernet:

DHCP automatically detected

No manual configuration required

If using WiFi:

Select SSID

Enter WiFi password

6. Storage Configuration

Select:

Use entire disk

Automatic partitioning

⚠️ Note: This will erase the previous operating system (Windows) and install Ubuntu Server as the primary OS.

7. Install OpenSSH Server (Critical Step)

During installation, select:

✔ Install OpenSSH Server

This enables:

Remote administration

SSH access from Kali Linux

Secure management from the monitoring laptop

Brute-force simulation testing

Log-based intrusion detection validation

This step is essential for a cybersecurity lab environment.

8. Final Installation Steps

After installation completes:

Remove USB flash drive

Press Enter to reboot

The system will now boot from the internal SSD.

You should see:

Ubuntu 22.04 LTS login:

At this stage, Ubuntu Server is successfully installed and ready for:

Docker installation

Monitoring stack deployment

Fail2ban configuration

SSH-based attack simulation
