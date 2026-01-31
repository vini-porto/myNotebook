# Definition

**Storage** refers to the hardware and technologies used to keep, maintain, and retrieve digital data on a long-term or permanent basis. 

>It is the digital equivalent of a filing cabinet or a warehouse where information sits until it is needed.

---
# Key Concepts

- **Non-Volatile Memory:** This is the defining characteristic of storage. It means data is not lost when the device loses power (unlike [[RAM]], which is "volatile").

- **[[SSD]] (Solid State Drive):** Modern storage that uses flash memory. It has no moving parts, making it incredibly fast and durable.

- **[[HDD]] (Hard Disk Drive):** Older technology that uses spinning magnetic platters and a physical read/write head. It is slower than SSDs but cheaper for storing massive amounts of data.

- **Capacity:** Measured in [[Bytes]] (Gigabytes, Terabytes, Petabytes), representing how much total information the device can hold.

- **Read/Write Speed:** How fast data can be pulled out of storage (Read) or saved onto it (Write).

# How it Works

Storage works by recording bits (0s and 1s) onto a physical medium in a way that can be "read" back later.

1. **Writing:** When you save a file, the [[Operating System]] sends a command to the storage controller to change the physical state of the medium (e.g., changing the magnetic polarity on an HDD or the electrical charge in an SSD cell).

2. **Retention:** The medium holds that physical state without needing constant electricity.

3. **Reading:** When you open the file, the controller detects those physical states and converts them back into digital signals for the [[CPU]] to process.

4. **[[File Systems]]:** To keep track of where data is, storage uses a "map" called a file system (like NTFS or APFS), which tells the computer exactly which "shelf" a piece of data is sitting on.

# Types of Storage

## Local Storage:

The internal [[SSD]] inside your laptop or the MicroSD card in your smartphone.

## External Storage:

USB flash drives or portable hard drives used for backups.

## [[Cloud Storage]]

Services like Google Drive or Dropbox. Even though this feels invisible, your data is physically stored on massive arrays of HDDs and SSDs in a remote data center.

## Enterprise Storage

Large businesses use **[[NAS]]** (Network Attached Storage) or **[[SAN]]** (Storage Area Network) to allow hundreds of computers to access the same central pool of data.

## Related Topics

- **[[Data Redundancy]]**
- **[[RAID]] (Redundant Array of Independent Disks)**
- **[[Object Storage]]**
- **[[Cold Storage]]**
- **[[Archiving]]**

# Tags

#study #learning #basics #storage #hardware