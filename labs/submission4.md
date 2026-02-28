# 1.

1. 

```
systemd-analyze
Startup finished in 7.518s (firmware) + 2.828s (loader) + 5.312s (kernel) + 11.465s (userspace) = 27.124s 
graphical.target reached after 11.433s in userspace.
```
```
systemd-analyze blame
31.188s apt-daily-upgrade.service
23.699s systemd-suspend.service
14.817s fstrim.service
 3.607s NetworkManager-wait-online.service
...
```
```
uptime
 16:58:52 up 5 days, 17:41,  1 user,  load average: 1.44, 1.17, 1.98
```
```
w
 16:59:05 up 5 days, 17:41,  1 user,  load average: 1.59, 1.21, 1.98
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU  WHAT
fateee   tty2     -                15:30    5days  0.01s  0.01s /usr/libexec/gn
```
```
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head -n 6
    PID    PPID CMD                         %MEM %CPU
  39280   38752 /snap/firefox/7836/usr/lib/ 12.1 24.2
  38548   37733 /snap/firefox/7836/usr/lib/  4.8 57.0
  38774   38752 /snap/firefox/7836/usr/lib/  2.9  1.3
  43914   43542 /usr/share/code/code /home/  2.3 10.9
  37733    3571 /usr/bin/gnome-shell         2.3 20.8
```
```
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head -n 6
    PID    PPID CMD                         %MEM %CPU
  38548   37733 /snap/firefox/7836/usr/lib/  4.8 56.9
  42864   42755 /usr/share/code/code --type  2.1 24.8
  39280   38752 /snap/firefox/7836/usr/lib/ 12.1 24.2
  37733    3571 /usr/bin/gnome-shell         2.3 20.8
  42979   42747 /proc/self/exe --type=utili  0.7 12.3
```
```
systemctl list-dependencies
default.target
● ├─accounts-daemon.service
● ├─gdm.service
● ├─gnome-remote-desktop.service
● ├─ollama.service
● ├─power-profiles-daemon.service
...
```
```
systemctl list-dependencies multi-user.target
multi-user.target
○ ├─anacron.service
● ├─apport.service
● ├─avahi-daemon.service
● ├─console-setup.service
● ├─containerd.service
...
```
```
who -a
           system boot  2026-02-17 23:17
           run-level 5  2026-02-17 23:18
fateee   ? seat0        2026-02-23 15:30   ?         37587 (login screen)
fateee   + tty2         2026-02-23 15:30  old        37587 (tty2)
```
```
last -n 5
fateee   tty2         tty2             Mon Feb 23 15:30   still logged in
fateee   seat0        login screen     Mon Feb 23 15:30   still logged in
fateee   tty2         tty2             Tue Feb 17 23:20 - 15:30 (5+16:10)
fateee   seat0        login screen     Tue Feb 17 23:20 - 15:30 (5+16:10)
reboot   system boot  6.14.0-37-generi Tue Feb 17 23:17   still running

wtmp begins Sat Nov 30 02:41:30 2024
```
```
free -h
               total        used        free      shared  buff/cache   available
Mem:            14Gi       8.1Gi       2.7Gi       128Mi       4.0Gi       6.9Gi
Swap:          4.0Gi        21Mi       4.0Gi
```
```
cat /proc/meminfo | grep -e MemTotal -e SwapTotal -e MemAvailable
MemTotal:       15706372 kB
MemAvailable:    7199052 kB
SwapTotal:       4194300 kB
```

2.

- The system takes 27 seconds to boot, with userspace taking the longest at 11.5 seconds, and the boot process is significantly slowed by several services with apt-daily-upgrade.service taking an unusually long 31 seconds to run.

- The system has been running continuously for over 5 days with a single user logged in, and while the load averages (1.44, 1.17, 1.98) indicate moderate system activity, the 5-day idle time on the display manager suggests the user is likely away from an active graphical session.

- Firefox processes dominate system resource usage, with one instance consuming 12.1% of memory and another using 57% CPU, while GNOME Shell and VS Code also contribute significantly to the overall system load.

- The system boots into a graphical (default.target) environment with GNOME-related services and Ollama running, while the multi-user.target shows a mix of essential system services along with container runtimes (containerd) and crash reporting tools (apport) configured to start at boot.

- The system was last booted on February 17th and has been running continuously for 5 days, with user fateee logging in at 15:30 today after a previous session lasting over 5 days, confirming the system's prolonged uptime and the user's recent return to an active session.

- The system has 14GB of RAM with 8.1GB currently used, but 6.9GB is still available thanks to 4GB of cached memory, while swap usage is minimal at only 21MB out of 4GB total.

3. 

The top memory-consuming process is a Firefox process (PID 39280) using 12.1% of memory.

4.

Firefox dominates both memory and CPU usage with multiple processes, while GNOME Shell and VS Code also contribute consistently to system load, indicating a typical desktop workload with web browsing and development activities.

# 2.

1.

```
traceroute github.com
traceroute to github.com (140.82.121.3), 30 hops max, 60 byte packets
 1  _gateway (192.168.0.1)  2.510 ms  2.439 ms  2.392 ms
 2  10.16.255.152 (10.16.255.152)  7.198 ms  7.156 ms  7.109 ms
 3  10.16.238.38 (10.16.238.38)  7.583 ms 10.16.238.78 (10.16.238.78)  10.656 ms 10.16.238.94 (10.16.238.94)  7.493 ms
 4  10.16.248.150 (10.16.248.150)  7.784 ms  7.738 ms 10.16.248.218 (10.16.248.218)  7.686 ms
 5  10.16.248.189 (10.16.248.189)  13.930 ms * 10.16.248.134 (10.16.248.134)  8.126 ms
 ...
```
```
dig github.com

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> github.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51756
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;github.com.			IN	A

;; ANSWER SECTION:
github.com.		29	IN	A	140.82.121.4

;; Query time: 7 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Feb 23 17:09:11 MSK 2026
;; MSG SIZE  rcvd: 55
```
```
sudo timeout 10 tcpdump -c 5 -i any 'port 53' -nn
tcpdump: data link type LINUX_SLL2
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes

0 packets captured
0 packets received by filter
0 packets dropped by kernel
```
```
dig -x 8.8.4.4

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 47428
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.		IN	PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.	7658	IN	PTR	dns.google.

;; Query time: 7 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Feb 23 17:10:10 MSK 2026
;; MSG SIZE  rcvd: 73
```
```
dig -x 1.1.2.2

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> -x 1.1.2.2
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 28957
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;2.2.1.1.in-addr.arpa.		IN	PTR

;; AUTHORITY SECTION:
1.in-addr.arpa.		736	IN	SOA	ns.apnic.net. read-txt-record-of-zone-first-dns-admin.apnic.net. 23597 7200 1800 604800 3600

;; Query time: 66 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Feb 23 17:10:22 MSK 2026
;; MSG SIZE  rcvd: 137
```

2.

The network path to GitHub traverses through multiple private (10.x.x.x) and carrier-grade NAT hops before reaching international routing in Germany, with significant latency increases and packet loss occurring after hop 12, suggesting possible network congestion or filtering.

3.

DNS queries are being resolved quickly (7ms) through the local stub resolver (127.0.0.53), with no observed DNS traffic during the capture period indicating either cached responses or inactive DNS queries at that moment.

4.

The reverse lookup for 8.8.4.4 returns a successful NOERROR status but provides no answer section, indicating that while the DNS query was processed correctly, there is no PTR record configured for this IP address.

5.

Since no packets were captured by tcpdump, I cannot provide a specific DNS query example from the packet capture. If there were packets captured, I would extract a DNS query example by examining the tcpdump output.