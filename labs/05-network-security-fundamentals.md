# Lab 5: Network Security Fundamentals

**Duration:** 60-90 minutes  
**Difficulty:** Intermediate  
**Prerequisites:** Labs 1-3 completed

## Objectives
- Understand common network security threats
- Analyze open ports and services
- Implement basic security hardening
- Monitor suspicious network activity

## Tools Required
- netstat
- netsh
- Windows Defender Firewall
- Task Manager

## Lab Exercises

### Exercise 1: Port Scanning & Service Discovery

**Step 1:** Check all listening ports
```cmd
netstat -ano | findstr LISTENING
```

**Step 2:** Identify processes using ports
```cmd
netstat -anob
```

**Step 3:** List all TCP connections
```cmd
netstat -an -p TCP
```

**Analysis Questions:**
- Which ports are listening on 0.0.0.0?
- Are there any unexpected services running?
- Which processes have established external connections?

### Exercise 2: Firewall Configuration Review

**Step 1:** Check firewall status
```cmd
netsh advfirewall show allprofiles
```

**Step 2:** List firewall rules
```cmd
netsh advfirewall firewall show rule name=all
```

**Step 3:** View blocked connections
```cmd
netsh advfirewall show currentprofile logging
```

**Analysis Questions:**
- Is the firewall enabled on all profiles?
- Are there overly permissive rules?
- Where are firewall logs stored?

### Exercise 3: Network Connection Monitoring

**Step 1:** Monitor active connections in real-time
```cmd
netstat -ano 5
```

**Step 2:** Check for established connections to specific ports
```cmd
netstat -an | findstr :443
netstat -an | findstr :80
```

**Step 3:** Identify foreign addresses
```cmd
netstat -an | findstr ESTABLISHED
```

**Analysis Questions:**
- Are there connections to unexpected IP addresses?
- Which applications are making external connections?
- Are there any connections on non-standard ports?

### Exercise 4: Security Hardening

**Step 1:** Disable unnecessary services (example)
```cmd
sc query "RemoteRegistry"
sc config "RemoteRegistry" start=disabled
```

**Step 2:** Review network shares
```cmd
net share
```

**Step 3:** Check for null sessions
```cmd
net use \\127.0.0.1\IPC$ "" /user:""
```

**Analysis Questions:**
- Which services can be safely disabled?
- Are there unnecessary network shares?
- Is anonymous access restricted?

### Exercise 5: Threat Detection Basics

**Step 1:** Check for suspicious connections
```cmd
netstat -anob | findstr ESTABLISHED
```

**Step 2:** Review ARP cache for anomalies
```cmd
arp -a
```

**Step 3:** Check DNS cache for suspicious domains
```cmd
ipconfig /displaydns | findstr "Record"
```

**Analysis Questions:**
- Are there multiple MAC addresses for one IP?
- Are there connections to known malicious IPs?
- Are there suspicious DNS queries cached?

## Troubleshooting Scenarios

### Scenario 1: Unexpected Port Open
**Problem:** Port 4444 is listening but you don't recognize the service.

**Investigation Steps:**
1. `netstat -ano | findstr :4444`
2. Note the PID
3. `tasklist | findstr <PID>`
4. Investigate the process in Task Manager

### Scenario 2: Excessive Outbound Connections
**Problem:** A process is making hundreds of outbound connections.

**Investigation Steps:**
1. `netstat -ano | findstr ESTABLISHED`
2. Identify the PID with most connections
3. `tasklist /FI "PID eq <PID>"`
4. Check process legitimacy

## Best Practices
- Regularly audit open ports and services
- Keep firewall enabled on all network profiles
- Monitor outbound connections, not just inbound
- Disable unnecessary services and protocols
- Use strong authentication for network shares
- Review firewall logs periodically

## Key Takeaways
- Open ports are potential attack vectors
- Firewall configuration is critical for security
- Monitoring network activity helps detect threats
- Security is about layers of defense
- Regular audits prevent security drift

## Additional Resources
- Windows Security Baseline
- CIS Benchmarks for Windows
- NIST Cybersecurity Framework
- Common Ports Reference (IANA)

## Next Steps
Proceed to [Lab 6: Firewall Configuration](06-firewall-configuration.md) for advanced firewall management.
