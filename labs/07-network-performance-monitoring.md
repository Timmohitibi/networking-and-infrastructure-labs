# Lab 7: Network Performance Monitoring

**Duration:** 60-75 minutes  
**Difficulty:** Advanced  
**Prerequisites:** Labs 1-4 completed

## Objectives
- Monitor network performance metrics
- Identify bandwidth bottlenecks
- Analyze latency and packet loss
- Troubleshoot performance issues

## Tools Required
- ping
- pathping
- netstat
- perfmon (Performance Monitor)
- Resource Monitor

## Lab Exercises

### Exercise 1: Latency Analysis

**Step 1:** Basic latency test
```cmd
ping -n 100 8.8.8.8
```

**Step 2:** Continuous monitoring
```cmd
ping -t google.com
```

**Step 3:** Packet size testing
```cmd
ping -l 1472 8.8.8.8
ping -l 512 8.8.8.8
ping -l 64 8.8.8.8
```

**Analysis Questions:**
- What is the average latency?
- Is there packet loss?
- How does packet size affect latency?

### Exercise 2: Path Analysis

**Step 1:** Trace route with statistics
```cmd
pathping google.com
```

**Step 2:** Analyze specific hop
```cmd
pathping -h 15 -q 50 8.8.8.8
```

**Step 3:** Compare multiple paths
```cmd
pathping cloudflare.com
pathping aws.amazon.com
```

**Analysis Questions:**
- Where is the highest latency occurring?
- Which hop has packet loss?
- How many hops to destination?

### Exercise 3: Bandwidth Utilization

**Step 1:** Monitor network interface statistics
```cmd
netstat -e
```

**Step 2:** Check statistics over time (run multiple times)
```cmd
netstat -e -s
```

**Step 3:** Monitor specific protocol statistics
```cmd
netstat -s -p TCP
netstat -s -p UDP
netstat -s -p IP
```

**Analysis Questions:**
- How many bytes sent/received?
- Are there transmission errors?
- What is the error rate?

### Exercise 4: Connection Performance

**Step 1:** View all connections with statistics
```cmd
netstat -ano -p TCP
```

**Step 2:** Monitor connection state changes
```cmd
netstat -ano 5
```

**Step 3:** Check for retransmissions
```cmd
netstat -s | findstr -i "retrans"
```

**Analysis Questions:**
- How many active connections exist?
- Are there many TIME_WAIT connections?
- What is the retransmission rate?

### Exercise 5: Performance Monitor Setup

**Step 1:** Open Performance Monitor
```cmd
perfmon
```

**Step 2:** Add network counters (via GUI or command)
```cmd
typeperf "\Network Interface(*)\Bytes Total/sec" -sc 10
```

**Step 3:** Monitor specific metrics
```cmd
typeperf "\Network Interface(*)\Current Bandwidth" "\Network Interface(*)\Output Queue Length" -sc 20
```

**Key Counters to Monitor:**
- Network Interface\Bytes Total/sec
- Network Interface\Packets/sec
- Network Interface\Output Queue Length
- Network Interface\Packets Received Errors
- TCPv4\Segments Retransmitted/sec

### Exercise 6: Resource Monitor Analysis

**Step 1:** Open Resource Monitor
```cmd
resmon
```

**Step 2:** Navigate to Network tab

**Step 3:** Analyze:
- Processes with Network Activity
- Network Activity (bytes/sec)
- TCP Connections
- Listening Ports

**Analysis Questions:**
- Which process uses most bandwidth?
- Are there stalled connections?
- What is the total network utilization?

## Troubleshooting Scenarios

### Scenario 1: High Latency
**Problem:** Users report slow network performance.

**Investigation Steps:**
1. `ping -n 100 <gateway>` - Test local network
2. `ping -n 100 8.8.8.8` - Test internet
3. `pathping <destination>` - Identify problem hop
4. `netstat -s | findstr -i "error"` - Check for errors

**Common Causes:**
- Network congestion
- Faulty hardware
- ISP issues
- DNS problems

### Scenario 2: Packet Loss
**Problem:** Intermittent connectivity issues.

**Investigation Steps:**
1. `ping -n 500 <gateway>` - Test for local loss
2. `pathping <destination>` - Identify where loss occurs
3. `netstat -e` - Check interface errors
4. Check physical connections

**Common Causes:**
- Cable issues
- Network congestion
- Hardware failure
- Wireless interference

### Scenario 3: Bandwidth Saturation
**Problem:** Network feels slow during peak hours.

**Investigation Steps:**
1. Open Resource Monitor → Network tab
2. Identify top bandwidth consumers
3. `netstat -ano` - Check connection count
4. `typeperf "\Network Interface(*)\Bytes Total/sec"` - Monitor utilization

**Common Causes:**
- Large file transfers
- Streaming services
- Backup operations
- Malware/unwanted traffic

## Performance Baselines

### Establish Baseline Metrics
```cmd
REM Run during normal operations
ping -n 100 <gateway> > baseline-gateway.txt
ping -n 100 8.8.8.8 > baseline-internet.txt
netstat -e > baseline-stats.txt
pathping <key-server> > baseline-path.txt
```

### Compare Against Baseline
Run same commands during issues and compare results.

## Performance Optimization Tips

### Reduce Latency
- Use wired connections over wireless
- Minimize network hops
- Use geographically closer servers
- Optimize DNS resolution

### Improve Throughput
- Upgrade network hardware
- Reduce network congestion
- Optimize TCP window size
- Disable unnecessary protocols

### Reduce Packet Loss
- Check cable quality
- Update network drivers
- Reduce wireless interference
- Replace faulty hardware

## Advanced Monitoring

### Create Performance Log
```cmd
logman create counter NetworkPerf -f bin -v mmddhhmm -max 500 -c "\Network Interface(*)\*" -si 00:00:05
logman start NetworkPerf
REM Let it run...
logman stop NetworkPerf
```

### Export Statistics
```cmd
netstat -e > network-stats-%date%.txt
netstat -s >> network-stats-%date%.txt
```

## Best Practices
- Establish performance baselines
- Monitor during peak and off-peak hours
- Document normal vs. abnormal metrics
- Use multiple tools for correlation
- Test from multiple locations
- Keep historical data for trending
- Address issues proactively

## Key Takeaways
- Latency, bandwidth, and packet loss are key metrics
- Baseline measurements enable comparison
- Multiple tools provide complete picture
- Path analysis identifies problem locations
- Regular monitoring prevents issues

## Additional Resources
- Windows Performance Monitor documentation
- TCP/IP performance tuning guide
- Network troubleshooting methodology
- Bandwidth calculation formulas

## Next Steps
Apply learned skills to real-world network troubleshooting scenarios.
