tags: #forensics #acquisition

# Forensic Acquisition

links: [[702 DF TOC - Storage & Acquisition|DF TOC - Storage & Acquisition]] - [[themes/000 Index|Index]]

---
## Forensically Sound Acquisition

"**Forensically Sound** Acquisition" refers to the process of creating a digital copy of evidence that adheres to certain standards to ensure its integrity and admissibility in court. According to the NIST Computer Forensic Tool Testing (CFTT) standard, a forensically sound acquisition involves:

- **Completeness**: Ensuring that every accessible sector of a drive is copied.
- **Sector Range**: Copying from sector zero to the last sector of the drive.
- **Integrity**: No modification of the evidence drive during the acquisition process.
- **Error Logging**: Reporting and logging all I/O errors encountered.
- **Accurate Documentation**: Ensuring tool user documentation is correct.

These standards, although originating in the US, are internationally accepted, ensuring the forensic process is consistent and reliable across jurisdictions. For more information, visit the [CFTT website](http://www.cftt.nist.gov/).

## Digital Evidence Terminology

- **Forensically Sound**: Refers to evidence handled in a manner that ensures its integrity and admissibility in court.
- **Forensic Completeness**: Ensuring all relevant data is captured and preserved.
- **Forensic Acquisition**: The process of copying data from a digital device while maintaining its integrity.
- **Forensic Imaging**: Creating an exact bit-by-bit copy of digital media for analysis.
- **Digital Evidence**: Information stored or transmitted in binary form that may be relied upon in court.
- **Digital Traces**: Residual data left behind after digital activities, which can be analyzed.
- **Evidence Preservation**: Maintaining the integrity and availability of digital evidence over time.
- **Evidence Integrity**: Ensuring that the digital evidence remains unaltered and untampered.
- **Chain of Custody**: Documentation that details the handling, transfer, and storage of evidence to prevent contamination or tampering.

## Write Blocker

**Write Blockers** are essential tools in digital forensics to prevent data alteration on evidence drives.

**Why Use Write Blockers?**

- **Automated OS Processes**: Systems can automatically modify data through indexing, auto-mounting, antivirus scans, filesystem journaling, and RAID reassembly.
- **Human Error**: Mistakes like wrong commands or accidental drag-and-drop operations can alter evidence.
- **Standard Forensic Process**: Using write blockers is a best practice in forensics to ensure data integrity.

**Types of Write Blockers**

- **Hardware Write Blockers**: Physically prevent writing to the drive, providing reliable protection against data modification.
- **Software Write Blockers**: Implemented through software solutions, though they are harder to maintain and guarantee.

**Functions of a Write Blocker**

- **Interception of Commands**: Blocks dangerous commands that might alter data on the drive (supporting ATA, SCSI, NVMe interfaces).
- **Hardware Protection**: Ensures physical prevention of data writing.
- **Linux Kernel Flags**: Can be set to make a block device read-only.

**Applications**

Write blockers are used in various forensic tools, including portable kits, drive bays, and imaging appliances, to maintain the integrity of digital evidence during analysis and acquisition.


## Digital Evidence Preservation

Preserving the integrity of digital evidence is important in forensic investigations to ensure that the data remains unchanged and admissible in court.

**Key Points**

- **Nature of Digital Evidence**
    - Unlike physical objects (e.g., smoking guns, bloody knives), digital evidence does not use physical evidence bags.
    - Examples include disk images, memory dumps, and packet captures.
    - It is essential to prove that digital evidence has not been modified since collection.

**Methods to Preserve Integrity**

- **Cryptographic Techniques**
    
    - **Hashing**: Applying cryptographic hashing algorithms (such as MD5, SHA) to generate a unique hash value for the data.
    - **Signatures**: Using cryptographic signatures (like PGP, S/MIME) to sign the data.
    - These methods can be implemented as a separate step or integrated into forensic tools.
    - Cryptographic methods allow validation at a later time to confirm the data remains unchanged.
- **Validation**:
    
    - Recalculate the hash of the evidence at any point to verify it matches the original hash, thus confirming no changes have occurred.

Using these techniques ensures the reliability and integrity of digital evidence throughout the forensic process.

## Digital Evidence Validation

**Recalculating the Hash**

Recalculating the hash of digital evidence is not always sufficient for validation because:

- Disks can have errors.
- Changing a single bit invalidates the hash.
- Bad sectors can potentially render a disk image inadmissible in court.

**Piece-wise Hashing**

Piece-wise hashing, also known as hash windows, involves:

- Taking a hash of every n blocks.
- Allowing validation of most parts of the disk.
- Ensuring only some parts of a disk might be invalid as evidence.
- Creating a separate file with a list of hashes across the disk.

Piece-wise hashing is integrated into many forensic tools and formats, enhancing the reliability and admissibility of digital evidence in legal contexts.

## Compression

Forensic images are large and need careful planning due to their size and the time required to create them. They cover sectors from 0 to the last sector of the storage medium and can take hours or days to generate. Although many forensic file formats support compression, the `dd` tool does not. Some tools lack efficiency as they don’t support seeking and create temporary files instead.

## Squashfs: Compressed File System

Squashfs is a compressed, read-only file system used in forensics for storing and analyzing large data sets efficiently. It’s integrated into the Linux kernel, making it fast and multithreaded.

#### Benefits for Forensic Use:

- **Read-Only Nature**: Ensures the integrity of data. For example, if you have a forensic image stored in Squashfs, you can add new files such as logs or reports without altering the original image. This preserves the original data for accurate analysis.
- **Mounting Convenience**: Can be easily mounted as a filesystem, simplifying access to data.
- **Efficient Storage**: Employs block-level compression to handle large files efficiently, saving storage space.

Using Squashfs in forensics helps manage the typically large sizes of forensic images more effectively, making it easier and faster to handle and analyze data during investigations. For Linux users, the `sfsimage` tool can be utilized to work with Squashfs images, providing a practical solution for forensic analysis. More information is available at http://digitalforensics.ch/sfsimage/.

## Forensic Formats

In digital forensics, raw images of drives are often insufficient. Specialized forensic formats are used because they offer additional features and benefits:

- **Compression**: Reduces the size of forensic images, making storage and transfer more efficient.
- **Split Files**: Divides large images into smaller, manageable pieces.
- **Security**: Supports encrypted images to protect sensitive data.
- **Built-in Hashes and Logs**: Ensures data integrity and provides logs for auditing.
- **Metadata**: Allows the addition of notes, names of people, and case information, which aids in the investigation process.
- **Beyond Drive Images**: Some formats can include data from various sources, not just drive images.

### Popular Forensic Formats

- **EnCase EWF**: A commercial format known as the "Expert Witness" format. It is the oldest and widely used in forensics.
- **FTK SMART**: Another commercial format used in forensic investigations.
- **Afflib**: An open-source format known as the "Advanced Forensic Format," offering features comparable to commercial options.

## Managing Acquisition Issues

When acquiring forensic evidence, it's important to address both integrity validation and potential errors.

#### Validating Evidence Integrity

- **Store Separate Copy of Hashes**: Keep an independent copy of the hash values to verify the data's integrity later.
- **Confirm Hashes**: Regularly check that hash values match to ensure no data alteration.
- **Reassemble Split Files**: Ensure that all parts of split files are correctly reassembled to maintain data completeness.

#### Errors and Failures

- **Heat**: Excessive heat can cause hardware failures; maintain proper cooling.
- **Old Failing Disks**: Older disks might have bad blocks; handle them carefully.
- **Read Sectors Backwards**: In some cases, reading from the end of the disk to the beginning can avoid triggering bad sectors.
- **Kernel Errors**: Monitor system logs (e.g., `dmesg`, `journalctl`) for errors during the acquisition process.
- **Bad Cables**: Use high-quality, short cables to minimize signal degradation.
- **Data Recovery Tools**: Employ these tools to retrieve data from damaged or failing disks.

---
links: [[702 DF TOC - Storage & Acquisition|DF TOC - Storage & Acquisition]] - [[themes/000 Index|Index]]