# <span id='top'>Format USB</span>

[[Common Format]](#common)  
[[Diskpart Format]](#diskpart)  
[[References]](#ref)

<br>

## <span id='common'>Common Format</span>

[[Top]](#top)

### Windows 

1. Stick the USB drive to the computer. 
2. On the USB drive icon, menu-click > click on `Format (A)`.
3. Set configurations:

- File system (F): choose `NTFS`
  - NTFS: _NTFS—the primary file system for recent versions of Windows and Windows Server—provides a full set of features including security descriptors, encryption, disk quotas, and rich metadata, and can be used with Cluster Shared Volumes (CSV) to provide continuously available volumes that can be accessed simultaneously from multiple nodes of a failover cluster._ ([Microsoft](https://docs.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview)) _New Technology File System (NTFS) is a proprietary journaling file system developed by Microsoft. Starting with Windows NT 3.1, it is the default file system of the Windows NT family. It superseded File Allocation Table (FAT) as the preferred filesystem on Windows and is supported in Linux and BSD as well._ ([Wikipedia](https://en.wikipedia.org/wiki/NTFS))
Now you are all set to start. 

4. Click on `start`.

<br>

## <span id='diskpart'>Diskpart Format</span>

[[Top]](#top)

1. Run `Diskpart` and check for all connected storage. 

        DISKPART> list disk

          Disk ###     Status           Size     Free       Dyn  Gpt
          ----------  -------------  -------  ------------  ---  ---
          Disk 0       Online        119 GB       1024 KB        *
          Disk 1       Online         29 GB         29 GB
          Disk 2       Online         57 GB           0 B

2. Select disk. 

        DISKPART> select disk 2

        disk 2 is now the selected disk.

          Disk ###     Status           Size     Free       Dyn  Gpt
          ----------  -------------  -------  ------------  ---  ---
          Disk 0       Online        119 GB       1024 KB        *
          Disk 1       Online         29 GB         29 GB
        * Disk 2       Online         57 GB           0 B


3. Remove all partitions using: `clean`
    
        DISKPART> clean
        
        DiskPart succeeded in cleaning the disk. 

Now the USB drive can be re-initialised, partitioned, and formatted.

<img src="https://github.com/deep-woods/Utils/blob/main/images/diskpart01_clean.png" />

4. Now create a new main partition.

        DISKPART> create partition primary
        
        DiskPart created the selected partition.

5. Set the main partition active. 

        DISKPART> select partition 1
        
        Partition 1 is now the selected partition.
        
        DISKPART> active
        
        DiskPart set the current partition active.
        
6. Format the disk. 
       
        format label=[USB name] fs=[file format type] quick
        format label=SanDisk_Silver_64 fs=NTFS quick
        
          100 percent complete
          
        DiskPart successfully formatted the volume.

<img src="https://github.com/deep-woods/Utils/blob/main/images/diskpart02_format.png" />

<br>

### <span id='ref'>References</span>

[[Top]](#top)

- P_Emblem (2021) https://postiveemblem.tistory.com/261
- TechMeSpot (2019) How to Format USB Flash Drive on Windows 10? https://www.youtube.com/watch?v=NqGz6_php74&ab_channel=TechMeSpot
- SEAGATE https://www.seagate.com/kr/ko/support/kb/how-to-diskpart-eraseclean-a-drive-through-the-command-prompt-005929en/
