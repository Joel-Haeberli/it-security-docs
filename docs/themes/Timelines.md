tags: #DF #timelines
 
# Timelines

links: [[705 DF TOC - Encryption & Timelines & Find|DF TOC -Encryption & Timelines & Find]] - [[themes/000 Index|Index]]

---

## Overview

### Why Timelines?

> Exam question: Why are timelines important

Creating timelines is essential in digital forensics for several reasons:

- **Historical Analysis:** Timelines allow forensic analysts to go back in time and perform digital archaeology.
- **Reconstructing Events:** They help reconstruct past events to understand the sequence and context of actions.
- **Key Questions:** Timelines address the fundamental questions of who, what, where, when, and how.
- **Timestamps:** Utilizing various timestamps, timelines provide a detailed view of activities.
- **Accuracy and Correlation:** Although timestamps may not always be perfectly accurate, cross-referencing with multiple sources improves reliability.

### Time Representation

- **UNIX Epoch:** Represents time as the number of seconds since January 1, 1970, 00:00:00 UTC.
	- Example: `$ date +%s`
- **Global Formats:** Different regions use different date formats, which can lead to confusion.
	- Example: "1/2/21" can mean February 1 or January 2.
	- Common Swiss format: `dd.mm.year`
	- Recommended formats: ISO 8601 or RFC 3339 for consistency.
- **Standards and Time Zones:**
	- **Universal Coordinated Time (UTC):** A standard for timekeeping.
	- **Greenwich Mean Time (GMT):** A time zone.
	- **Linux Resources:** Use `man tzfile`, `man zdump`, or check `/usr/share/zoneinfo` for information on time zones.
- **Internet Time:**
- **Swatch ".beats":** Invented by Swatch, representing time in metric units with 1000 "beats" per day, formatted as "@123".
- **No Time Zones:** This system eliminates time zones and daylight saving adjustments.

## Filesystem Timestamps

Typical timestamps in filesystems include "MACB":

- **Modify (M):** Last time file contents were modified.
- **Access (A):** Last time file contents were accessed.
- **Change (C):** Last time attributes (inode or MFT) were changed.
- **Birth (B):** Time the file was originally created (not always available).

These timestamps depend on filesystem and OS configurations. Not all filesystems support a creation timestamp, and some have additional timestamps (e.g., HFS has a Backup timestamp). Operating systems can disable last accessed timestamps for performance reasons.

### Building Filesystem Timelines

Using Sleuthkit’s `mactime` tool, forensic analysts can create text-based timelines, with each timestamp on a new line. This tool takes "time machine" formatted input generated by other Sleuthkit commands:

- Generating time machine output:
	- `fls -m partition1 /dev/sda1`
	- `fls -m partition2 /dev/sda2`
	- `fls -m disk2 /dev/sdb1`
	- `ils -m /dev/sda1`
  
- Creating a timeline for analysis:
	- For CSV output: `fls -r -m partition1 /dev/sda1 | mactime -d`
	- For image files: `fls -r -m partition1 -o 2048 image.dd | mactime -d`
	- Combining outputs: `cat fls1.out fls2.out fls3.out | mactime -d`

### Challenges with Timestamps

Timestamps can be problematic due to:

- **Clock Drift and Skew:** Inconsistent timekeeping in devices.
- **OS Delays:** Non-real-time updates and granularity issues.
- **Timezones:** Determining the correct timezone (GMT, UTC, local).
- **Global Investigations:** Handling multiple timezones.
- **Daylight Savings and Leap Years:** Regions switch at different times; handling leap years and leap seconds (IERS).
- **Malicious Changes:** Anti-forensic techniques like timestomp.

Sleuthkit offers flags to adjust timestamps:
- **Adjusting Seconds:** `-s seconds` to add/subtract seconds.
- **Specifying Timezone:** `-z zone` to set the timezone (e.g., CET).

Always verify timestamps with caution due to potential errors and anti-forensic activities.

## Building Supertimelines

A supertimeline aggregates timestamps from multiple sources, including:

- **Filesystem Timestamps:** MACB timestamps.
- **Logs:** Syslog, MS event logs, application logs, firewall logs, AV logs.
- **Browser Data:** History, cookies, cache, bookmarks.
- **Windows Artifacts:** Registry, prefetch files, LNK files, recycle bin.
- **Emails:** PST, MBOX, Maildir formats.
- **Documents:** Office files, PDFs, OpenOffice docs.
- **Metadata:** EXIF data from images and videos.
- **Memory Dumps:** Volatility output files.
- **Network Traffic:** Captured PCAP files.
- **Physical Sources:** CCTV, badge readers, phone logs.
- **Other Sources:** Mobile phones, IoT devices, cloud services.

The `log2timeline/plaso` framework, written in Python, is a comprehensive tool for creating supertimelines.

---

links: [[705 DF TOC - Encryption & Timelines & Find|DF TOC -Encryption & Timelines & Find]] - [[themes/000 Index|Index]]