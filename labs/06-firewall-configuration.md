# Lab 6: Firewall Configuration

**Duration:** 45-60 minutes  
**Difficulty:** Advanced  
**Prerequisites:** Lab 5 completed

## Objectives
- Configure Windows Defender Firewall rules
- Manage inbound and outbound traffic
- Implement port-based filtering
- Test firewall effectiveness

## Tools Required
- netsh
- Windows Defender Firewall with Advanced Security
- telnet/Test-NetConnection (PowerShell)

## Lab Exercises

### Exercise 1: Firewall Rule Management

**Step 1:** View current firewall state
```cmd
netsh advfirewall show allprofiles state
```

**Step 2:** Enable firewall on all profiles
```cmd
netsh advfirewall set allprofiles state on
```

**Step 3:** List existing rules
```cmd
netsh advfirewall firewall show rule name=all | more
```

**Analysis Questions:**
- How many rules are currently configured?
- Which profile is most restrictive?
- Are there any disabled rules?

### Exercise 2: Creating Inbound Rules

**Step 1:** Block specific port
```cmd
netsh advfirewall firewall add rule name="Block Port 8080" dir=in action=block protocol=TCP localport=8080
```

**Step 2:** Allow specific application
```cmd
netsh advfirewall firewall add rule name="Allow MyApp" dir=in action=allow program="C:\Path\To\App.exe" enable=yes
```

**Step 3:** Allow port range
```cmd
netsh advfirewall firewall add rule name="Allow Ports 5000-5010" dir=in action=allow protocol=TCP localport=5000-5010
```

**Verification:**
```cmd
netsh advfirewall firewall show rule name="Block Port 8080"
```

### Exercise 3: Creating Outbound Rules

**Step 1:** Block outbound to specific IP
```cmd
netsh advfirewall firewall add rule name="Block IP 203.0.113.0" dir=out action=block remoteip=203.0.113.0
```

**Step 2:** Allow outbound on specific port
```cmd
netsh advfirewall firewall add rule name="Allow HTTPS Out" dir=out action=allow protocol=TCP remoteport=443
```

**Step 3:** Block all outbound for application
```cmd
netsh advfirewall firewall add rule name="Block App Outbound" dir=out action=block program="C:\Path\To\App.exe"
```

### Exercise 4: Advanced Rule Configuration

**Step 1:** Create rule with specific profile
```cmd
netsh advfirewall firewall add rule name="Public Block" dir=in action=block protocol=TCP localport=445 profile=public
```

**Step 2:** Create rule for specific interface
```cmd
netsh advfirewall firewall add rule name="LAN Only" dir=in action=allow protocol=TCP localport=3389 profile=private
```

**Step 3:** Enable logging
```cmd
netsh advfirewall set allprofiles logging filename %systemroot%\system32\LogFiles\Firewall\pfirewall.log
netsh advfirewall set allprofiles logging maxfilesize 4096
netsh advfirewall set allprofiles logging droppedconnections enable
```

### Exercise 5: Testing Firewall Rules

**Step 1:** Test blocked port (PowerShell)
```powershell
Test-NetConnection -ComputerName localhost -Port 8080
```

**Step 2:** Verify rule is blocking
```cmd
netstat -an | findstr :8080
```

**Step 3:** Check firewall logs
```cmd
type %systemroot%\system32\LogFiles\Firewall\pfirewall.log | more
```

## Troubleshooting Scenarios

### Scenario 1: Application Cannot Connect
**Problem:** Application fails after enabling firewall.

**Resolution Steps:**
1. Identify application executable path
2. Check if rule exists: `netsh advfirewall firewall show rule name=all | findstr "AppName"`
3. Create allow rule for application
4. Test connectivity

### Scenario 2: Rule Not Working
**Problem:** Created rule but traffic still passes.

**Resolution Steps:**
1. Verify rule is enabled
2. Check rule priority and conflicts
3. Ensure correct profile is active
4. Review rule parameters (port, protocol, direction)

### Scenario 3: Remote Desktop Blocked
**Problem:** Cannot RDP after firewall changes.

**Resolution Steps:**
```cmd
netsh advfirewall firewall add rule name="Allow RDP" dir=in action=allow protocol=TCP localport=3389 profile=private
```

## Common Firewall Rules

### Block Common Attack Ports
```cmd
netsh advfirewall firewall add rule name="Block SMB" dir=in action=block protocol=TCP localport=445
netsh advfirewall firewall add rule name="Block NetBIOS" dir=in action=block protocol=TCP localport=139
netsh advfirewall firewall add rule name="Block RDP Public" dir=in action=block protocol=TCP localport=3389 profile=public
```

### Allow Essential Services
```cmd
netsh advfirewall firewall add rule name="Allow DNS" dir=out action=allow protocol=UDP remoteport=53
netsh advfirewall firewall add rule name="Allow HTTP" dir=out action=allow protocol=TCP remoteport=80
netsh advfirewall firewall add rule name="Allow HTTPS" dir=out action=allow protocol=TCP remoteport=443
```

## Rule Management

### Delete Rule
```cmd
netsh advfirewall firewall delete rule name="Block Port 8080"
```

### Disable Rule
```cmd
netsh advfirewall firewall set rule name="Block Port 8080" new enable=no
```

### Export Configuration
```cmd
netsh advfirewall export "C:\firewall-backup.wfw"
```

### Import Configuration
```cmd
netsh advfirewall import "C:\firewall-backup.wfw"
```

### Reset to Defaults
```cmd
netsh advfirewall reset
```

## Best Practices
- Default deny for inbound, selective allow for outbound
- Use specific rules over broad rules
- Document all custom rules
- Test rules before deploying to production
- Regular backup of firewall configuration
- Enable logging for troubleshooting
- Use profiles appropriately (Domain, Private, Public)
- Remove unused rules periodically

## Key Takeaways
- Firewall rules control traffic flow
- Direction (in/out) and action (allow/block) are critical
- Profile-specific rules enhance security
- Testing validates rule effectiveness
- Logging aids in troubleshooting

## Additional Resources
- Windows Firewall with Advanced Security documentation
- Netsh AdvFirewall command reference
- Common port numbers (IANA registry)

## Next Steps
Proceed to [Lab 7: Network Performance Monitoring](07-network-performance-monitoring.md) for performance analysis.
