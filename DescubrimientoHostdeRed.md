# Penstesting de Red

- <https://book.hacktricks.wiki/es/generic-methodologies-and-resources/pentesting-network/index.html#discovering-hosts>

## Desubrimientos de host desde el exterior

***Trasas ICMP**

***
ping -c 1 199.66.11.4    # 1 echo request to a host
fping -g 199.66.11.0/24  # Send echo requests to ranges
nmap -PE -PM -PP -sn -n 199.66.11.0/24 #Send echo, timestamp requests and subnet mask requests
***

## Descubrimiento de Puerto TCP

- Usamo masscan para buscar puertos abiertos

***Nos Enfocamos en los Servicios HTTP***

***masscan -p20,21-23,25,53,80,110,111,135,139,143,443,445,993,995,1723,3306,3389,5900,8080 199.66.11.0/24***

## Descubrimiento de Puertos UDP

- Verificamos si hay puertos UPD abiertos

***nmap -sU -sV --version-intensity 0 -F -n 199.66.11.53/24***

- The -sV will make nmap test each possible known UDP service packet

- The "--version-intensity 0" will make nmap only test the most probable

## Descubrimientos de Host desde Adentro

- sirver para descubrir host dentro de la red que esta disponibles

***Pasivo***

- se utiliza esta herramienta para descubrir pasivamente host dentro de una red conectada

- netdiscover -p
- p0f -i eth0 -p -o /tmp/p0f.log
- net.recon on/off
- net.show
- set net.show.meta true

***Activo***

Descubrimientos hosts desde afuera ejemplo puertos TCP/HTTP/UDP/SCTP

# ARP discovery

nmap -sn <Network> #ARP Requests (Discover IPs)
netdiscover -r <Network> #ARP requests (Discover IPs)

# NBT discovery

nbtscan -r 192.168.0.1/24 #Search in Domain

# Bettercap

net.probe on/off #Discover hosts on current subnet by probing with ARP, mDNS, NBNS, UPNP, and/or WSD

set net.probe.mdns true/false #Enable mDNS discovery probes (default=true)

set net.probe.nbns true/false #Enable NetBIOS name service discovery probes (default=true)

set net.probe.upnp true/false #Enable UPNP discovery probes (default=true)

set net.probe.wsd true/false #Enable WSD discovery probes (default=true)

set net.probe.throttle 10 #10ms between probes sent (default=10)

# IPv6

alive6 <IFACE> # Send a pingv6 to multicast.

## Escaneo de Hosts

- una vez se descubren la ip(externas o internas) se pueden realizar diferentes acciones

# Nmap fast scan for the most 1000tcp ports used

- nmap -sV -sC -O -T4 -n -Pn -oA fastscan <IP>

# Nmap fast scan for all the ports

- nmap -sV -sC -O -T4 -n -Pn -p- -oA fullfastscan <IP>

# Nmap fast scan for all the ports slower to avoid failures due to -T4

- nmap -sV -sC -O -p- -n -Pn -oA fullscan <IP>

# Bettercap Scan

- syn.scan 192.168.1.0/24 1 10000 #Ports 1-10000
