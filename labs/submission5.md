# 1. 

1. Ubuntu 24.04.3 LTS 

2. VirtualBox Graphical User Interface Version 7.0.16_Ubuntu

# 2.

1. CPU Details: Processor model, architecture, cores, frequency

- model name   : AMD Ryzen 7 4800 with Radeon Graphics (from cat /proc/cpuinfo)
- architecture : x86_64 (from uname -m)
- cores        : 4 (from cat /proc/cpuinfo)
- frequency    : 1794.714 (from cat /proc/cpuinfo)

2. Memory Information: Total RAM, available memory

- Total RAM        : 8130672 kB (from cat /proc/meminfo)
- available memory : 6981908 kB (from cat /proc/meminfo)

3. Network Configuration: IP addresses, network interfaces

- IP addresses       : 10.0.2.15 (from ip -br addr)
- network interfaces : lo, enp0s3 (from ip -br addr)

4. Storage Information: Disk usage, filesystem details

- Disk usage         : Size: 40G, Used: 11G, Avail: 27G (from df -h)
- filesystem details : types: tmpfs, ext4. used: 11m+ (from df -T)

5. Operating System: Ubuntu version, kernel information

- Ubuntu version     : Ubuntu 24.04.4 LTS (from lsb_release -a)
- kernel information : Linux devops-VirtualBox 6.17.0-14-generic... GNU/Linux (from uname -a)

6. Virtualization Detection: Confirmation system is running in a VM

- systemd-detect-virt outputs oracle, which means my system is indeed is running in an Oracle VM VirtualBox machine.

### The /proc filesystem proved most useful for CPU and memory details, providing direct access to hardware information through /proc/cpuinfo and /proc/meminfo, while the ip command was invaluable for network configuration with its clean, concise output format, and systemd-detect-virt was the most straightforward tool for confirming virtualization, clearly identifying the Oracle VM environment with a single command.