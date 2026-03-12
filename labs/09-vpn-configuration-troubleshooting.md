# Lab 9: VPN Configuration & Troubleshooting

**Duration:** 60–120 minutes  
**Difficulty:** Advanced  
**Track:** VPN  
**Prerequisites:** Labs 1–4 completed (recommended)

## Objective
Understand the most common VPN failure modes (DNS, routing, MTU, authentication, firewall/NAT) and learn a systematic troubleshooting approach.

## Safety / scope notes
- Only connect to VPNs you own or have permission to use.
- Do not test against production networks unless explicitly authorized.

## Lab environment
You’ll need one of the following:
- An existing VPN you can connect to (work/home lab), or
- A local lab VPN server (WireGuard/OpenVPN) you control

## Exercises

### Exercise 1: Pre-VPN baseline
- Record: local IP, default gateway, DNS servers, public IP (if allowed), and current routes.
- Verify: can reach a public IP and resolve a domain.

### Exercise 2: Connect VPN + verify tunnel
- Confirm tunnel interface exists and has an IP.
- Verify what changed: routes, DNS, and public IP (split vs full tunnel).

### Exercise 3: Common failure isolation matrix
Test in this order and document results:
1. Can you reach a public IP? (Layer 3)
2. Can you resolve DNS? (Name resolution)
3. Can you reach an internal/private target by IP?
4. Can you reach the same target by name?

### Exercise 4: MTU and fragmentation symptoms
- Identify “some sites work, others hang” behavior.
- Test with smaller packet sizes and note what succeeds/fails.

## Troubleshooting scenarios
### Scenario 1: VPN connects but no internal access
- Likely causes: missing routes, split-tunnel config, firewall rules on server-side, wrong allowed-ips/push routes.

### Scenario 2: Internal access works by IP but not by name
- Likely causes: VPN DNS not applied, DNS suffix/search domain missing, or DNS is blocked over tunnel.

### Scenario 3: Access is intermittent / slow
- Likely causes: MTU issues, unstable WAN, or UDP blocked causing fallback/encapsulation problems.

## Expected results
- A clear written checklist to debug VPN issues quickly (baseline → tunnel verify → routing → DNS → MTU).

## Key takeaways
- Most “VPN is broken” reports reduce to **routing**, **DNS**, **MTU**, or **firewall/NAT**.

## Next steps
Add a follow-up lab for your chosen VPN technology (e.g. WireGuard deep dive, OpenVPN deep dive).
