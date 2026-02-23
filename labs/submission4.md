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