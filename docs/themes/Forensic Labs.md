tags: #forensics #lab #tools 

# Forensic Labs

links: [[707 DF TOC - Labs & Tools|DF TOC - Labs & Tools]] - [[themes/000 Index|Index]]

---

**Document the filesystem (separate for each partition)**

1. **How many blocks are allocated?**
   - Use the `fsstat` command from Sleuth Kit to display filesystem statistics, including the number of allocated blocks.
   ```sh
   fsstat /path/to/image
   ```

2. **How many normal files and directories?**
   - Use the `fls` command to list files and directories, then count them.
   ```sh
   fls -r /path/to/image | grep 'r/' | wc -l  # Count regular files
   fls -r /path/to/image | grep 'd/' | wc -l  # Count directories
   ```

3. **How many deleted files and directories?**
   - Again, use `fls` with the `-d` option to list deleted files and directories.
   ```sh
   fls -r -d /path/to/image | wc -l
   ```

**Sectors and blocks**

1. **Choose a random sector number inside a partition**
   - Use a hex editor like `xxd` to view a sector.
   ```sh
   xxd -s $((sector_number * 512)) -l 512 /path/to/image
   ```

2. **View the sector with a hex editor**
   - You can use `xxd` as shown above to view the sector data in hexadecimal.

3. **In what filesystem block is the sector?**
   - Use `blkcat` from Sleuth Kit to map a sector to a filesystem block.
   ```sh
   blkcat -o partition_offset -b block_size /path/to/image sector_number
   ```

4. **Is the block allocated?**
   - Use `blkls` to list allocated blocks.
   ```sh
   blkls /path/to/image
   ```

5. **If yes, what is the file name?**
   - Use `fls` and `icat` to find the file name associated with the inode.
   ```sh
   fls -r /path/to/image | grep inode_number
   ```

**Document the files in one filesystem**

1. **Choose a filename (from fls -r)**
   - Use `fls` to list files recursively.
   ```sh
   fls -r /path/to/image
   ```

2. **What is the inode or MFT number?**
   - The `fls` output includes the inode number.

3. **How many blocks does it use?**
   - Use `istat` to get inode information, including the number of blocks used.
   ```sh
   istat /path/to/image inode_number
   ```

4. **What is the logical file size?**
   - The `istat` command output includes the logical file size.

5. **Extract the file**
   - Use `icat` to extract the file.
   ```sh
   icat /path/to/image inode_number > output_file
   ```

6. **Extract the file slack**
   - Use `blkls` and `icat` together to extract slack space.
   ```sh
   blkls -s /path/to/image | icat /path/to/image inode_number > file_slack
   ```

7. **What are the timestamps?**
   - `istat` provides detailed timestamp information (access, modification, creation times).

**Deleted files**

1. **Find a deleted file (from fls -r)**
   - Use `fls -r -d` to list deleted files.
   ```sh
   fls -r -d /path/to/image
   ```

2. **Is it already overwritten?**
   - Use `istat` to check if the inode or data blocks have been reused.

3. **Recover the file (if possible)**
   - Use `icat` to recover the deleted file if it has not been overwritten.
   ```sh
   icat /path/to/image inode_number > recovered_file
   ```

---
links: [[707 DF TOC - Labs & Tools|DF TOC - Labs & Tools]] - [[themes/000 Index|Index]]