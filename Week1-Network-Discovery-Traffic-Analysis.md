
# Network Discovery & Traffic Analysis — Week 1

## Objective

Perform basic network reconnaissance and establish a baseline of normal network traffic using Kali Linux, Nmap, and Wireshark.

## Lab Environment

- Operating System: Kali Linux
- Virtualization: VirtualBox
- Network Mode: Bridged Adapter
- Network Interface: eth0
- Tools: Nmap 7.99, Wireshark

## 1. Network Configuration

The Kali Linux virtual machine was initially configured with a Host-Only Adapter. To allow the VM to communicate with the local network, the adapter was changed to a Bridged Adapter.

Network configuration was verified using:

```bash
ip addr
````

The Kali VM received a local network address in the `192.168.104.0/24` subnet.

The default gateway was identified using:

```bash
ip route
```

This confirmed that Kali was successfully connected to the local network.

## 2. Network Discovery with Nmap

A host discovery scan was performed against the local `/24` network:

```bash
nmap -sn 192.168.104.0/24
```

The scan identified three active hosts on the network.

The gateway host was subsequently checked for available services:

```bash
nmap 192.168.104.38
```

The scan identified TCP port 53 as open, indicating that a DNS-related service was available on the gateway.

A second discovered host was also enumerated:

```bash
nmap 192.168.104.42
```

TCP port 53 was identified as open, while the majority of the remaining TCP ports were filtered.

## 3. Neighbor Discovery

The local neighbor table was reviewed using:

```bash
ip neigh
```

This displayed discovered devices, their associated IP addresses, network interface, and MAC addresses.

This helped correlate the hosts identified during Nmap discovery with devices visible at the local network layer.

## 4. Wireshark Traffic Baseline

Wireshark was used to capture normal network traffic through the `eth0` interface.

The capture produced:

* Packets captured: 228
* Packets dropped: 0

The following protocols were observed:

* QUIC
* TCP
* TLS 1.2
* TLS 1.3
* ARP

The traffic was predominantly encrypted, with TLS and QUIC accounting for a significant portion of the observed application traffic. ARP traffic was also observed as expected for local network address resolution.

## Findings

The exercise successfully demonstrated the basic workflow for network reconnaissance and traffic analysis:

1. Configure Kali Linux for local network connectivity.
2. Verify IP addressing and routing.
3. Identify active hosts using Nmap.
4. Enumerate basic services and open ports.
5. Review local network neighbors.
6. Capture and analyze normal network traffic using Wireshark.

## Key Learning Outcomes

This exercise improved my understanding of:

* IPv4 addressing and CIDR notation
* Default gateways and network routing
* Bridged networking in VirtualBox
* Host discovery with Nmap
* Ports and network services
* MAC address and neighbor discovery
* Packet capture and protocol analysis
* Encrypted network traffic
* Establishing a normal traffic baseline for security monitoring

## Conclusion

The network discovery and traffic analysis exercise provided practical experience with identifying hosts and services on a controlled network and analyzing normal network communications.

The combination of Nmap and Wireshark provided a basic foundation for further security monitoring, network enumeration, and incident investigation activities.

