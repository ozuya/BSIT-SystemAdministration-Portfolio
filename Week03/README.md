# Week 03 - Enterprise Server Deployment and Operating System Installation

**Student:** Cedrick Gayoso  
**Program:** Bachelor of Science in Information Technology (BSIT)  
**Course:** ITEP 414 - System Administration and Maintenance  
**Section:** BSIT-4E  
**Week:** 3  
**Project Type:** Individual Portfolio Project  
**Project Title:** Enterprise Server Deployment and Operating System Installation

> **Current status (16 August 2026):** Ubuntu Server installation and all required verification tasks are complete. Windows Server 2025 Standard Evaluation (Desktop Experience) is installed, renamed to `winserver01`, and verified through successful Administrator login. Screenshot evidence 01-15 is included. Remaining external steps: update/publish the GitHub repository and post the LinkedIn reflection.

## Project Overview
This Week 3 portfolio project follows the course scenario of a Junior System Administrator at **ABC Startup Solutions** deploying the company's first Linux server. The Ubuntu Server is intended as a baseline for future file sharing, remote administration, database hosting, web hosting, and internal services. The project includes Ubuntu Server installation, configuration, verification, BIOS-versus-UEFI research, an Ubuntu boot-process flowchart, a Windows Server Evaluation bring-home activity, an operating-system comparison, and professional technical documentation.

## Learning Objectives
- Explain the purpose of an operating system in enterprise environments.
- Differentiate BIOS and UEFI firmware.
- Explain the stages of the computer boot process.
- Compare Ubuntu Server, Windows Server, and Rocky Linux.
- Install Ubuntu Server in a virtual machine.
- Configure server settings during installation.
- Enable secure remote administration using SSH.
- Verify server functionality.
- Document installation procedures and produce professional technical documentation.

## Software Requirements
- Oracle VirtualBox
- Ubuntu Server ISO used in the lab: `ubuntu-26.04-live-server-amd64.iso`
- Windows Server Evaluation ISO for the bring-home activity

## Virtual Machine Specifications and Actual Lab Values
| Component | Required / Actual Configuration |
|---|---|
| Name | `Ubuntu-Server-Week03` |
| RAM | 4 GB / 4096 MB |
| CPU | 2 virtual processors |
| Storage | 40 GB VDI, dynamically allocated |
| Network | NAT |
| Optical Drive | Ubuntu Server ISO |
| Language | English |
| Keyboard | English (US) |
| Network configuration | DHCP |
| IPv4 address | `10.0.2.15/24` on `enp0s3` |
| Hostname | `server01` |
| Administrative user | `sedo` (non-root) |
| Disk method | Guided - Use Entire Disk with LVM |
| Filesystem | `ext4` for `/` and `/boot` |
| SSH | OpenSSH Server installed; service verified `active (running)` |
| Additional packages | None selected |

## Installation Summary
1. Created the `Ubuntu-Server-Week03` VM with 4 GB RAM, 2 virtual processors, a 40 GB dynamically allocated VDI, NAT networking, and the Ubuntu Server ISO.
2. Selected **English** as the installation language and **English (US)** for the keyboard layout.
3. Accepted DHCP; `enp0s3` received `10.0.2.15/24`.
4. Selected the standard Ubuntu Server installation and did not select third-party drivers.
5. Left the proxy field blank and used the Ubuntu archive configuration.
6. Selected **Use an entire disk** and retained LVM. The storage summary showed `ext4` for `/boot` and the root logical volume.
7. Created the non-root administrative account `sedo` and assigned hostname `server01`.
8. Skipped Ubuntu Pro for now.
9. Enabled **Install OpenSSH server** and password authentication.
10. Did not install additional packages.
11. Completed installation, removed the installation ISO when prompted, and rebooted into the installed server.

## Configuration Summary
- Hostname: `server01`
- User: Cedrick Gayoso / username `sedo`
- Network: DHCP through VirtualBox NAT
- IPv4 address: `10.0.2.15/24`
- Disk: 40 GB VDI, Guided - Use Entire Disk, LVM
- Filesystems observed: `ext4` for `/` and `/boot`
- OpenSSH Server: installed and running
- Additional packages: none selected

## Verification Results
| Verification | Command | Result |
|---|---|---|
| Login | Local login | Successful as `sedo` |
| Hostname | `hostname` | `server01` |
| IP address | `ip addr` | `10.0.2.15/24` on `enp0s3` |
| Internet connectivity | `ping -c 4 google.com` | 4 transmitted, 4 received, 0% packet loss |
| System update | `sudo apt update` and `sudo apt upgrade -y` | Completed successfully after mirror troubleshooting |
| SSH service | `systemctl status ssh` | `active (running)` verified in live VM |

## Screenshot Evidence
- `screenshots/01-virtualbox-vm-settings.png`
- `screenshots/02-ubuntu-language.png`
- `screenshots/03b-installation-type.png`
- `screenshots/03-ubuntu-keyboard.png`
- `screenshots/04-network-configuration.png`
- `screenshots/05a-guided-storage.png`
- `screenshots/05-storage-configuration.png`
- `screenshots/06-profile-setup.png`
- `screenshots/07-openssh-installation.png`
- `screenshots/08-ubuntu-login.png`
- `screenshots/09-hostname-verification.png`
- `screenshots/10-ip-address-verification.png`
- `screenshots/11-ping-test.png`
- `screenshots/12-system-update.png`
- `screenshots/13-ssh-status.png`
- `screenshots/14-windows-server-installation.png`
- `screenshots/15-windows-server-login.png`

## BIOS vs UEFI Highlights
The project comparison covers definition, boot process, maximum disk support, partition style, security features, speed, advantages, disadvantages, and modern usage. The complete comparison and one-page explanation are provided in `BIOS_vs_UEFI.pdf`.

## Ubuntu Boot Process Flowchart
![Ubuntu Boot Process](diagrams/BootProcessFlowchart.png)

**Power On -> BIOS/UEFI Initialization -> Boot Device Detection -> Boot Loader (GRUB) -> Linux Kernel -> init/systemd -> Services Start -> Login Prompt**

The flowchart is exported as both `BootProcessFlowchart.pdf` and `diagrams/BootProcessFlowchart.png`.

## Windows Server Installation Summary
Windows Server 2025 Standard Evaluation (Desktop Experience) was installed in a separate VirtualBox VM with 4 GB RAM, 2 virtual CPUs, a 50 GB VDI, NAT networking, and the Windows Server Evaluation ISO. A VirtualBox `BLKCACHE_IOERR` occurred while host storage was low; after freeing host space and resetting the VM once, installation completed. An Administrator password was created, login succeeded, and the computer was renamed to `winserver01`.

Evidence:
- `screenshots/14-windows-server-installation.png`
- `screenshots/15-windows-server-login.png`

## Operating System Comparison
The comparison of **Windows Server**, **Ubuntu Server**, and **Rocky Linux** across licensing, user interface, package management, security, performance, enterprise use cases, advantages, and disadvantages is provided in `OS_Comparison.pdf`.

## Editable Source Documents
Editable Word source documents are included in `editable/`. The boot-process flowchart remains editable through `diagrams/boot_process.dot`.

## Challenges Encountered
1. **Duplicate VDI registration:** A second VM creation attempt failed because a virtual disk with the same name/UUID was already registered. The duplicate creation was stopped and the correct VM was retained.
2. **Missing/inaccessible VDI:** VirtualBox reported `VERR_FILE_NOT_FOUND` for `Ubuntu-Server-Week03.vdi`. The invalid disk attachment was replaced with a new 40 GB dynamically allocated VDI on SATA Port 0.
3. **Settings-save issue:** VirtualBox temporarily failed to save VM settings while the VM state/storage configuration was inconsistent. Returning the VM to a clean powered-off state and repairing storage resolved the issue.
4. **CPU soft-lockup message:** Ubuntu displayed a soft-lockup watchdog warning during package installation. The installation was monitored instead of being forcibly stopped and eventually completed successfully.
5. **Ubuntu package mirror 403:** `apt upgrade` initially failed with `403 Forbidden` while fetching a firmware package from the Philippine archive mirror. After changing the archive URI to the main Ubuntu archive and rerunning `apt update` and `apt upgrade -y`, the update completed successfully.
6. **Command typo during SSH verification:** `systemct1` was typed with the number `1` instead of lowercase `l`. The correct `systemctl status ssh` command confirmed that the SSH service was active and running.
7. **Windows Server VirtualBox I/O cache error:** VirtualBox raised `BLKCACHE_IOERR` while the host drive was low on free space. Host storage was freed, the VM was reset once, and Windows Setup continued successfully.

## Reflection
This Week 3 project demonstrated that a server deployment is not complete when the operating system merely finishes installing. The server also needs a consistent identity, networking, storage layout, secure administration, maintenance, verification, and documentation. For the ABC Startup Solutions scenario, I configured the Ubuntu Server VM with the required 4 GB of RAM, two virtual processors, 40 GB of storage, NAT networking, hostname `server01`, non-root user `sedo`, LVM storage, and OpenSSH Server.

The verification phase turned the installation settings into measurable evidence. I successfully logged in after reboot, confirmed the hostname with `hostname`, verified the `10.0.2.15/24` address using `ip addr`, and tested Internet connectivity with four successful replies from `google.com` and 0% packet loss. I also performed `sudo apt update` and `sudo apt upgrade -y`. The upgrade process introduced another real troubleshooting situation because the Philippine Ubuntu mirror returned a `403 Forbidden` error for one firmware package. Changing the archive source to the main Ubuntu archive and repeating the update allowed the upgrade to finish successfully. Finally, `systemctl status ssh` confirmed that the SSH service was active and running.

The VirtualBox problems were equally useful. I encountered a duplicate VDI registration, a missing VDI file, and a settings-save issue before the installation could proceed reliably. Later, the Ubuntu installer displayed a CPU soft-lockup warning. These problems reinforced the importance of reading error messages carefully, avoiding unnecessary destructive actions, and making controlled changes one at a time.

The BIOS-versus-UEFI comparison and Ubuntu boot-process flowchart helped connect hardware startup to operating-system services. Understanding the path from firmware initialization to GRUB, the Linux kernel, systemd, services, and the login prompt gives a practical framework for diagnosing startup problems. Overall, this activity strengthened my understanding of installation, verification, troubleshooting, security, and technical documentation as connected responsibilities in system administration.

## References
- Ubuntu Server official documentation.
- Microsoft Windows Server official documentation and Evaluation resources.
- Rocky Linux official documentation.
- UEFI Forum specifications and documentation.
