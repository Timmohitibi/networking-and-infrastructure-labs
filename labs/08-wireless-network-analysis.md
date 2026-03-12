# Lab 8: Wireless Network Analysis

**Duration:** 60–90 minutes  
**Difficulty:** Intermediate  
**Track:** Wireless  
**Prerequisites:** Labs 1–4 completed (recommended)

## Objective
Learn a repeatable workflow to diagnose common Wi‑Fi issues (weak signal, interference, roaming problems, driver/config issues) using built-in OS tools.

## Lab environment
- Non-production network only
- You should have access to your Wi‑Fi router/AP admin page (optional but helpful)

## Tools (choose what applies)
- Windows: `netsh wlan`, Settings UI, Event Viewer
- Linux: `iw`, `iwconfig`/`nmcli`, `rfkill`, `ip`, `ping`
- Optional: a second client device for comparison tests

## Exercises

### Exercise 1: Baseline signal + link info
- Capture SSID, band (2.4/5/6 GHz), channel, RSSI/signal %, link speed, and adapter/driver details.
- Document: distance to AP, obstacles, and whether you’re on power saving mode.

### Exercise 2: Interference and channel symptoms
- Compare results when moving closer/farther from the AP.
- If possible, compare 2.4 GHz vs 5 GHz on the same SSID (or separate SSIDs).

### Exercise 3: Throughput vs latency sanity checks
- Run a latency test to your gateway and a public IP (e.g., \(100\) pings).
- Note jitter and packet loss.

### Exercise 4: Roaming / sticky client check (optional)
- If you have multiple APs/mesh nodes, walk between them and observe if/when the client roams.
- Document when performance degrades and whether the client stays attached to a distant AP.

## Troubleshooting scenarios
### Scenario 1: “Good signal but slow”
- Check band, channel width, negotiated PHY rate, and whether you’re connected to 2.4 GHz unintentionally.

### Scenario 2: “Disconnects every few minutes”
- Check power saving, driver updates, and RF interference patterns.

## Expected results
- A written baseline you can compare against later (signal, band/channel, latency/jitter, basic throughput observation).

## Key takeaways
- Wi‑Fi issues usually separate into RF (signal/interference) vs config/driver vs upstream WAN constraints.

## Next steps
Proceed to [Lab 9: VPN Configuration & Troubleshooting](09-vpn-configuration-troubleshooting.md).
