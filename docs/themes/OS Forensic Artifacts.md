tags: #DF #artifact

# OS Forensic Artifacts

links: [[themes/704 DF TOC - Forensic Artifacts|DF TOC - Forensic Artifacts]] - [[themes/000 Index|Index]]

---

## Overview

OS forensic analysis examines the base OS components, looking for evidence of tampering, misuse, or artifacts that can shed light on digital events. This includes analyzing logs, system files, and application data to reconstruct activities or detect anomalies.

**Software packages**

- **Initial install:** Includes timestamps, OS version, base/add-on packages, and updates. These artifacts provide a timeline and components of the initial system setup.
- **Installed software packages:** Formats include deb, rpm, flatpak, msi, and dmg. These logs show what software was added post-initial setup.
- **Removed software packages:** Install logs and downloaded package files help track what has been uninstalled, indicating changes over time.
- **Self-contained bundles:** These are portable apps like those in MacOS, AppImage, and other similar formats. They can show usage of applications that do not require traditional installation.

**System and kernel**

- **OS and kernel version:** Knowing these versions is crucial to understanding the environment and potential vulnerabilities.
- **Kernel config/parameters:** Configuration details can affect system behavior and security settings.
- **Boot sequence:** This includes UEFI, boot loader, kernel, and system initialization processes, which are key to understanding how the system starts.
- **Startup services/daemons:** Managed by systemd, launchctl, or sysvinit, these services run automatically on boot and can be points of persistence for malware.
- **Boot up and shutdown times, hibernate, sleep:** These logs help establish timelines of system activity and potential user behavior.

**Note:** For most of these artifacts, specialized forensic tools are not necessary. A solid understanding of the operating system, its logs, and file structures suffices for analysis.

**Scheduled jobs/tasks**

- **cron/at:** Unix-based job schedulers used for automating tasks at specified times.
- **systemd timers:** Used in systems running systemd for scheduling tasks.
- **Windows schtasks:** Task scheduler for automating tasks in Windows environments.
- **User and system jobs:** Distinction between tasks initiated by users and those set by the system, which is important for forensic analysis.

**Human user activity**

- **Users and groups:** Information on user accounts and group memberships.
- **Logins, logouts:** Records of user sessions help establish timelines and access patterns.
- **Home directories, user files:** User-specific data and file modifications indicate user actions and preferences.
- **User permissions and security:** Access controls and security settings provide insights into user capabilities and potential security breaches.
- **Human proximity indicators:** Data that suggests the physical presence or actions of users, like key presses, mouse movements, opening laptop, fingerprint, face-login, celphone tower logs, lid closed, usb stick attached

**Note:** Distinguishing between human and system activity can be challenging but is crucial for accurate forensic analysis.

**Logs give historical timeline (if not modified)**

- **System logs:** Include dmesg, syslog, and journalctl. These logs provide detailed information about system events and errors.
- **MS Windows event logs:** Linux tools like grokevt and libevtx can be used to read these logs, which record system and application events in Windows.
- **Log files:** Typically found in `/var/log/*`, these files store a variety of system and application logs, crucial for forensic analysis.

**OS configuration**

- **Traditional Unix/Linux:** Configuration files located in `/etc` directory.
- **MS Windows registry:** The registry holds configuration settings and can be analyzed using Linux tools like registry-tools and reglookup.
- **gconf/dconf, plist files, systemd units:** These files and units store configuration settings for applications and services.
- **Dot files:** Located in xdg directories such as `.config`, `.local`, and `.cache`, these files store user-specific settings and caches.
- **Network configuration:** Includes settings for DNS, proxy, and VPN, which can show network behavior and connections.
- **Disk configuration:** Information about RAID, encryption, and attached devices, which help understand data storage and security measures.
- **Automounted local and remote drives/shares:** Details about automatically mounted drives and network shares provide insights into accessible resources and potential data sources.

**OS files interesting for forensics**

- **Temporary files and directories:** Locations like `/tmp` (clear at reboot) and `/var/tmp` (survive reboot) contain temporary data that can provide clues about recent activities.
- **Cache files, prefetch files:** These files store recently accessed data and application usage patterns.
- **Crash dumps, error report files:** Generated during system or application crashes, these files can help identify issues and their causes.
- **Hibernation files:** Contain the state of the system when it hibernates, useful for understanding system state at a particular time.

**Application layer OS data**

- **Clipboard data/history:** Records of copied content, which can reveal user actions.
- **Last used documents:** Tracks recently accessed files, providing insight into user activity.
- **Recycle bin, trash cans:** These store deleted files temporarily, allowing recovery of recently removed data.
- **OS search queries, index, thumbnails:** These logs show what users searched for, as well as indexed and previewed files $\rightarrow$ deleted files can stay in the index!

**Note:** The distinction between OS and application data can be blurry, but both are need for forensic analysis.

**OS specialty items**

- **Personal assistants (Cortana, Siri):** These assistants log voice commands and interactions, which can provide insights into user activity and preferences.
- **Proprietary file transfer (Apple AirDrop):** Tracks files transferred via AirDrop, including timestamps and recipient information.
- **Attached synced devices, backup (Time Machine):** Logs related to devices synced with the system and backups can show data transfers and backup routines.
- **Closely integrated OS applications:** Applications tightly integrated with the OS, like certain mail clients or calendars, leave extensive logs and usage data.
- **Fingerprints, face recognition:** Biometric data used for authentication can indicate user presence and access patterns.

**Cloud activity**

- **Cloud sync, backup:** Logs of data synced with and backed up to cloud services provide a record of what data was transferred and when.
- **Cached OS cloud artifacts:** Data temporarily stored locally before being uploaded to the cloud can show recent user actions.
- **VM instances, distributed/cloud nodes:** Virtual machine logs and details about distributed systems or cloud nodes can provide information on additional environments used.
- **VDI instances, thin clients:** Logs from Virtual Desktop Infrastructure instances and thin clients, which indicate usage of remote desktop services.

---
links: [[themes/704 DF TOC - Forensic Artifacts|DF TOC - Forensic Artifacts]] - [[themes/000 Index|Index]]