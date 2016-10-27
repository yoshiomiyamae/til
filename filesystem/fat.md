FAT
===

FAT is a filesystem that advocated by Microsoft.
This is the abbreviation of **File Allocation Table**

The original document can be downloaded from [Here](https://msdn.microsoft.com/en-us/windows/hardware/gg463080.aspx)

## FAT12 / FAT16
The numbers 12 and 16 indicates the number of table element bits.

### Volume structure
| Type | Name | Size [sectors] | Start Address [sectors] | Description |
|:--|---|---|---|--:|
| Reserved Area | Boot Sector | `1` | `0` | Including a boot information such as BPB |
| FAT Area | FAT | `BPB_FATSz16 * BPB_NumFATs` | `BPB_RsvdSecCnt` | Filesystem information |
| Directory Area | Root Directory | `(BPB_RootEntCnt * 0x20 + BPB_BytesPerSec -1) / BPB_BytesPerSec` | `BPB_FATSz16 * BPB_NumFATs + BPB_RsvdSecCnt`   | Storing the directories information |
| Data Area | Clasters | `BPB_NumClus * BPB_SecPerClus` | `(BPB_RootEntCnt * 0x20 + BPB_BytesPerSec -1) / BPB_BytesPerSec + BPB_FATSz16 * BPB_NumFATs + BPB_RsvdSecCnt` | Storing the files information |
| Data Area | Undefined | `BPB_TotSec - (BPB_RootEntCnt * 0x20 + BPB_BytesPerSec -1) / BPB_BytesPerSec + BPB_FATSz16 * BPB_NumFATs + BPB_RsvdSecCnt` | `BPB_NumClus * BPB_SecPerClus + (BPB_RootEntCnt * 0x20 + BPB_BytesPerSec -1) / BPB_BytesPerSec + BPB_FATSz16 * BPB_NumFATs + BPB_RsvdSecCnt` | Undefined |

### BPB (BIOS Parameter Block) structure
| Name | Size [bytes] | Start Address [bytes] | Description |
|:--|---|---|--:|
| BS_JmpBoot | `3` | `0` |  |
| BS_OEMName | `8` | `3` |  |
| BPB_BytsPerSec | `2` | `11` |  |
| BPB_SecPerClus | `1` | `13` |  |
| BPB_RsvdSecCnt | `2` | `14` |  |
| BPB_NumFATs | `1` | `16` |  |
| BPB_RootEntCnt | `2` | `17` |  |
| BPB_TotSec16 | `2` | `19` |  |
| BPB_Media | `1` | `21` |  |
| BPB_FATSz16 | `2` | `22` |  |
| BPB_SecPerTrk | `2` | `24` |  |
| BPB_NumHeads | `2` | `26` |  |
| BPB_HiddSec | `4` | `28` |  |
| BPB_TotSec32 | `4` | `32` |  |
| BS_DrvNum | `1` | `36` |  |
| BS_Reserved1 | `1` | `37` |  |
| BS_BootSig | `1` | `38` |  |
| BS_VolID | `4` | `39` |  |
| BS_VolLab | `11` | `43` |  |
| BS_FilSysType | `8` | `54` |  |
