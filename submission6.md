# Operating Systems & Networking Lab

## Task 1: Operating System Analysis

1. Analyze System Boot Time

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ systemd-analyze
Startup finished in 3.721s (firmware) + 3.240s (loader) + 3.672s (kernel) + 12.872s (userspace) = 23.506s 
graphical.target reached after 12.819s in userspace

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ systemd-analyze blame
6min 18.405s apt-daily-upgrade.service
      8.511s plymouth-quit-wait.service
      6.484s NetworkManager-wait-online.service
      3.833s fstrim.service
      2.577s postgresql@14-main.service
      2.143s snapd.seeded.service
      2.141s binfmt-support.service
      ...
```

2. Check System Load and Uptime

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ uptime
 22:17:44 up  2:05,  1 user,  load average: 0,56, 0,65, 0,58

igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ w
 22:17:45 up  2:05,  1 user,  load average: 0,59, 0,66, 0,58
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
igor     :1       :1               23:12   ?xdm?  20:35   0.00s /usr/libexec/gdm-x-session --run-script env GNOME_SHELL_SESSION_MODE=ubuntu /usr/bin/gnome-session --session=ubuntu
```

## Task 2: Networking Analysis

1. Traceroute

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ traceroute acm.timus.ru
traceroute to acm.timus.ru (212.193.69.18), 30 hops max, 60 byte packets
 1  XiaoQiang (192.168.31.1)  2.771 ms  2.698 ms  2.644 ms
 2  10.242.1.1 (10.242.1.1)  2.607 ms  2.571 ms  2.534 ms
 3  10.250.0.2 (10.250.0.2)  5.883 ms  2.463 ms  5.810 ms
 4  10.252.6.1 (10.252.6.1)  5.770 ms  5.732 ms  5.697 ms
 5  1.123.18.84.in-addr.arpa (84.18.123.1)  15.042 ms  101.524 ms  14.970 ms
 6  188.170.164.138 (188.170.164.138)  8.988 ms  89.183 ms  89.116 ms
 7  * * *
 8  188.170.164.9 (188.170.164.9)  88.967 ms  88.930 ms  14.389 ms
 9  pe03.ekaterinburg.gldn.net (79.104.240.211)  25.315 ms  28.726 ms  25.276 ms
10  195.239.186.162 (195.239.186.162)  33.592 ms  28.681 ms  101.964 ms
11  * * *
12  * * *
13  * * *
14  * * *
15  212.193.69.18 (212.193.69.18)  102.176 ms !X  105.171 ms !X  98.872 ms !X
```

2. Dig

```
igor@igor-HP-Pavilion-Gaming-Laptop-15-ec1xxx:~/Sum24-intro-labs$ dig acm.timus.ru

; <<>> DiG 9.18.18-0ubuntu0.22.04.2-Ubuntu <<>> acm.timus.ru
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14235
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;acm.timus.ru.			IN	A

;; ANSWER SECTION:
acm.timus.ru.		210	IN	A	212.193.69.18

;; Query time: 0 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Wed Jun 26 22:20:04 MSK 2024
;; MSG SIZE  rcvd: 57
```
