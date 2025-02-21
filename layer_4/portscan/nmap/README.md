# 🚚 Network Mapper (nmap)

```
 ________   _____ ______   ________  ________   
|\   ___  \|\   _ \  _   \|\   __  \|\   __  \  
\ \  \\ \  \ \  \\\__\ \  \ \  \|\  \ \  \|\  \ 
 \ \  \\ \  \ \  \\|__| \  \ \   __  \ \   ____\
  \ \  \\ \  \ \  \    \ \  \ \  \ \  \ \  \___|
   \ \__\\ \__\ \__\    \ \__\ \__\ \__\ \__\   
    \|__| \|__|\|__|     \|__|\|__|\|__|\|__|   
```

## 📖 Introduction

`nmap` is a tool that can be used to scan for clients in a network or also scan for open ports on a certain host. In this document I will demonstrate common use cases for `nmap`. In order to demonstrate certain applications, I use my [Kaindorf-Cafeteria-Box](https://github.com/FloDevAT/Kaindorf-Cafeteria-Box) with a network created using Docker.

### Scanning Networks

`nmap` can be used to search for ip addresses on a network with a simple command like this:

```bash
nmap -sN 192.168.100.0/24
```

In this example I use the `-sN` flag, which indicates that we want to scan a whole network instead of just a single host.

This would result in following output:

```
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-13 11:24 CET
Nmap scan report for 192.168.100.10
Host is up (0.000019s latency).
Not shown: 999 closed tcp ports (reset)
PORT     STATE         SERVICE
4000/tcp open|filtered remoteanything
MAC Address: 02:42:C0:A8:64:0A (Unknown)

Nmap done: 256 IP addresses (2 hosts up) scanned in 4.44 seconds
```

As we can see, this contains information about the hosts found and also some details information about services running on them.

### Scanning for Top Ports (UDP + TCP)

In the next example, we already obtained the IP adress of the host we want to scan and we want to search for the most common ports on the device. We can use following command for this:

```bash
nmap -sT -sU --top-ports 100 192.168.100.10
```

Here we use `-sT` which scans for TCP ports, `-sU` which scans for UDP ports and `--top-ports 100` which searches for the 100 most common ports. In our case it would not return anything, since port 4000 is not common / well-known port.

### Scanning Aggressive

```

```