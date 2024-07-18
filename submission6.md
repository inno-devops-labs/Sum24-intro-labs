# Operating Systems & Networking Lab

## Task 1: Operating System Analysis

![boot-reference](./assets/boot-reference.png)

From the observations, the system took a total of **33.273** seconds to boot.

The slowest component to boot was the **NetworkManager-wait-online** service and the fastest to boot was the **networking** service

![uptime-reference](./assets/uptime-reference.png)

The screenshot above shows the system's total uptime of **1 day, 21 mins** with an average CPU load of 1.64 (or 164%) in the last minute interval, 1.40 (140%) in the last 5 minutes interval and 1.18 (118%) in the 15 minutes interval

## Task 2: Networking Analysis

![Trace route](./assets/traceroute-reference.png)

From the traceroute output we can see that it takes about 8 hops to get to the destination. There are also no packet losses.

![Dig](./assets/dig-reference.png)

From the screenshot, the question (or query) was for A records of `kimfom.space` website and the answer provided the ip address associated with the domain: `216.24.57.1`