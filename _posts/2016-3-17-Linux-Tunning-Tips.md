---
layout: post
title: Linux Tunning Tips
tags: 性能测试 Linux
categories: 性能测试 Linux
---

## Linux Tunning Tips ##
1. **CPU core(s)** should not be consistently saturated. Use tools such as vmstat, top, atop, nmon,
perf, SystemTap, etc.
2. Generally, physical memory should never be saturated and the operating system should not page
memory out to disk. Use tools such as free, vmstat, /proc/meminfo, top, atop, nmon, etc.
3. Input/Output interfaces such as network cards and disks should not be saturated, and should not
have poor response times. Use tools such as df, stat, iostat, netstat, ping, nfsiostat, etc.
4. TCP/IP and network tuning, whilst sometimes complicated to investigate, may have dramatic
effects on performance. Tune TCP/IP socket buffers such as net.core.\*mem\* and
net.ipv4.tcp_\*mem\*.
5. Operating system level statistics and optionally process level statistics should be periodically
monitored and saved for historical analysis. Use tools such as atop.
6. Review operating system logs for any errors, warnings, or high volumes of messages. Review
logs such as /var/log/messages, /var/log/syslog, etc.
7. Review snapshots of process activity, and for the largest users of resources, review per thread
activity. Use tools such as top -H.
8. If the operating system is running in a virtualized guest, review the configuration and whether
or not resource allotments are changing dynamically. Review CPU steal time in tools such as
vmstat, top, etc.
9. Review `sysctl -a` for any uncommon kernel settings.
