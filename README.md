# Server Tuning

## Goal

This project aims to identify optimal system configurations to accelerate server performance. However, the challenge lies in the high diversity of tasks and the vast number of possible configuration combinations, making this problem complex and costly to solve through brute-force exploration.

---

## Observations

* Different tasks may require the same configuration settings.
   
E.g., both video downloading and backup tasks require similar configuration settings.

--- 
## Approach

1. **Classify Tasks**  
   Use performance counters to identify and classify the I/O pattern of each task.

2. **Tune System Settings Based on Classification**  
   For each I/O pattern class, apply tailored configuration adjustments known to be effective for that type.

---

## Environment Setting
- **Server**: HPE ProLiant DL380 Gen10 Plus  
- **CPU**: 2 × Intel Xeon Gold 5317  
- **DRAM**: 4 × 32 GB DDR4  
- **System**: Windows Server 2022 Datacenter  
- **Storage**: 3 × 6.4 TB NVMe SSDs  
