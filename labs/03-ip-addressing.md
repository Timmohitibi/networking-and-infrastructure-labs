# Lab 3: IP Addressing & Subnetting

## Objective
Practice IP addressing, subnetting, and network calculations.

## Prerequisites
- Calculator (or subnet calculator)
- Understanding of binary/decimal conversion

## Exercises

### Exercise 1: Network Information Discovery
```cmd
# Get current IP configuration
ipconfig

# Detailed network info
ipconfig /all

# Identify network class and subnet
# Document: IP, Subnet Mask, Default Gateway, Network ID
```

### Exercise 2: Subnet Calculations
Given network: 192.168.1.0/24

**Calculate:**
- Network address: `192.168.1.0`
- Broadcast address: `192.168.1.255`
- Usable host range: `192.168.1.1 - 192.168.1.254`
- Number of hosts: `254`

**Subnetting Practice:**
Divide 192.168.1.0/24 into 4 subnets:
- Subnet 1: `192.168.1.0/26` (hosts 1-62)
- Subnet 2: `192.168.1.64/26` (hosts 65-126)
- Subnet 3: `192.168.1.128/26` (hosts 129-190)
- Subnet 4: `192.168.1.192/26` (hosts 193-254)

### Exercise 3: Network Connectivity Testing
```cmd
# Test local network connectivity
ping 192.168.1.1

# Test subnet connectivity
ping 192.168.1.100

# Test gateway connectivity
ping [default_gateway_ip]

# Test internet connectivity
ping 8.8.8.8
```

### Exercise 4: ARP Table Analysis
```cmd
# View ARP table
arp -a

# Clear ARP cache
arp -d *

# Ping device and check ARP entry
ping 192.168.1.1
arp -a | findstr "192.168.1.1"
```

## Practice Problems
1. What subnet mask gives you exactly 30 usable hosts?
2. How many /27 subnets fit in a /24 network?
3. What's the broadcast address for 10.0.50.0/23?

## Verification Commands
```cmd
# Verify routing
route print

# Check network adapter settings
netsh interface ip show config
```