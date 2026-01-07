# Lab 4: Local Network Diagnostics

## Objective
Use Windows diagnostic tools to troubleshoot local network connectivity issues.

## Prerequisites
- Local network access
- Administrative privileges recommended

## Exercises

### Exercise 1: Network Interface Analysis
```cmd
# List all network adapters
ipconfig /all

# Show adapter statistics
netsh interface ip show interface

# Display adapter details
wmic path win32_networkadapter get name,speed,macaddress
```

### Exercise 2: Connectivity Testing Matrix
```cmd
# Test Layer 1-3 connectivity
ping 127.0.0.1          # Loopback (TCP/IP stack)
ping [local_ip]         # Local interface
ping [default_gateway]  # Local network
ping 8.8.8.8           # Internet connectivity
ping google.com        # DNS + Internet
```

### Exercise 3: Port and Service Analysis
```cmd
# Show listening ports
netstat -an | findstr LISTENING

# Show established connections
netstat -an | findstr ESTABLISHED

# Display process information
netstat -ano

# Check specific port
netstat -an | findstr :80
```

### Exercise 4: Network Path Analysis
```cmd
# Trace network path
tracert google.com

# Test with pathping (combines ping + tracert)
pathping google.com

# Check routing table
route print
```

### Exercise 5: Advanced Diagnostics
```cmd
# Network adapter troubleshooting
netsh wlan show profiles          # WiFi profiles
netsh interface show interface   # Interface status

# Reset network stack (if needed)
netsh winsock reset
netsh int ip reset

# Renew IP configuration
ipconfig /release
ipconfig /renew
```

## Troubleshooting Scenarios

### Scenario 1: No Internet Access
1. Check physical connection
2. Verify IP configuration
3. Test gateway connectivity
4. Check DNS resolution
5. Test external connectivity

### Scenario 2: Slow Network Performance
1. Check interface speed/duplex
2. Test bandwidth with ping flood
3. Analyze network utilization
4. Check for packet loss

### Scenario 3: Intermittent Connectivity
1. Monitor connection stability
2. Check for IP conflicts
3. Analyze DHCP lease
4. Test cable integrity

## Documentation Template
For each scenario, document:
- Symptoms observed
- Tests performed
- Results obtained
- Root cause identified
- Resolution applied