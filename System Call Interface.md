## 💻 [table for all system calls available](https://filippo.io/linux-syscall-table)
## [linux System call .h file](https://elixir.bootlin.com/linux/latest/source/include/linux/syscalls.h)
## System Call Analysis

### Introduction
System calls are the interface between user programs and the operating system. Analyzing these calls provides insights into how commands interact with the OS.

### Commands Analyzed
 
- `ps`: Displays information about running processes.  
- `cd`: Changes the current directory.
- `ls`: Lists directory contents.

<img align="left" width="31%" src="https://github.com/user-attachments/assets/77978dae-26db-4a3b-ad7c-2c6f34a5b118"/>
<img align="left" width="31%" src="https://github.com/user-attachments/assets/54279b28-5505-48ff-991f-e8a412002b3e"/>
<img align="left" width="31%" src="https://github.com/user-attachments/assets/51df1d19-2b74-49a8-806f-491b0201d9ff"/>

### Tracing Method
We used `strace` to trace system calls:
- **ps:** `strace -T -o ps_time.txt ps`
- ![image](https://github.com/user-attachments/assets/faee55e0-d97b-4e71-8edd-23cf75ce9a68)

- **cd:** `strace -T -o cd_time.txt bash -c "cd /desired/path"`
- ![image](https://github.com/user-attachments/assets/20e8bdea-8467-43a5-a6c7-6393ce6d151d)


- **ls:** `strace -T -o ls_time.txt ls`
- ![image](https://github.com/user-attachments/assets/b8ff80b8-d25a-4a9e-9539-2b499ca14264)

- ![image](https://github.com/user-attachments/assets/8a21d327-398e-4b9b-b8c6-025c61700aae)



### System Calls Summary
- **ps:** Involves system calls like `open`, `read`, `write`, `stat`, and `mmap`.
- **cd:** Utilizes `chdir`, `stat`, and `openat`.
- **ls:** Uses `open`, `readdir`, `close`, and `stat`.

### Performance Analysis
- The most time-consuming calls were `open` and `stat`, reflecting the need to access file metadata.
- `ps` made the most system calls, with `mmap` contributing significantly to its execution time.
  
### Other commands



