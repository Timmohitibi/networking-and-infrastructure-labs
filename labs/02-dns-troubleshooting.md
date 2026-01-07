# Lab 2: DNS Troubleshooting

## Objective
Diagnose and resolve common DNS issues using Windows tools.

## Prerequisites
- Administrative privileges
- Internet connectivity

## Exercises

### Exercise 1: Basic DNS Resolution
```cmd
# Test basic resolution
nslookup example.com

# Query specific record types
nslookup -type=MX example.com
nslookup -type=NS example.com
nslookup -type=A example.com
```

### Exercise 2: DNS Cache Management
```cmd
# View DNS cache
ipconfig /displaydns

# Clear DNS cache
ipconfig /flushdns

# Test resolution after flush
nslookup example.com
```

### Exercise 3: DNS Server Testing
```cmd
# Test different DNS servers
nslookup example.com 8.8.8.8
nslookup example.com 1.1.1.1

# Set specific DNS server
nslookup
> server 8.8.8.8
> example.com
```

### Exercise 4: Troubleshooting Scenarios
```cmd
# Simulate DNS failure
# 1. Set invalid DNS server
# 2. Test resolution
# 3. Restore working DNS

# Check DNS configuration
ipconfig /all | findstr "DNS Servers"
```

## Common Issues & Solutions
- **Slow resolution**: Check DNS server response times
- **NXDOMAIN errors**: Verify domain spelling and existence  
- **Timeout errors**: Test alternative DNS servers
- **Cache issues**: Clear DNS cache and test

## Lab Results
Document your findings for each exercise and note any resolution differences between DNS servers.