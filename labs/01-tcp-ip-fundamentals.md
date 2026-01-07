# Lab 1: TCP/IP Fundamentals

## Objective
Understand TCP/IP stack layers and analyze network traffic using command-line tools.

## Prerequisites
- Windows command prompt or PowerShell
- Basic understanding of networking concepts

## Exercises

### Exercise 1: Examine Network Stack
```cmd
# View network configuration
ipconfig /all

# Display routing table
route print

# Show active connections
netstat -an
```

### Exercise 2: TCP vs UDP Analysis
```cmd
# Test TCP connection
telnet google.com 80

# Test UDP (DNS query)
nslookup google.com

# Monitor connections during tests
netstat -an | findstr :80
netstat -an | findstr :53
```

### Exercise 3: Packet Analysis
```cmd
# Trace route to destination
tracert google.com

# Ping with different packet sizes
ping -l 1472 google.com
ping -l 1473 google.com
```

## Expected Results
- Understand MTU discovery
- Observe TCP 3-way handshake behavior
- Identify UDP vs TCP characteristics

## Troubleshooting Notes
- If telnet fails, check Windows features
- Large ping packets may fragment
- Tracert shows hop-by-hop path