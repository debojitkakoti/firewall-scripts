### Firewall script repository

### Prevent DDOS attack

This script enable rate limit for ssh to prevent DDOS.

Here is the steps performed in the script:

1. Flush all rules from all chains.
2. Delete user added empty chains.
3. Drop all packets not explicityly accepted.
4. Accept packets that are part of communications already. To prevent disconnecting from remote machine through ssh while applying the rule.
5. Check if SSH connection is tried to made from same IP within 60 seconds more than 3 times, if yes DROP it. It also checks for IP spoofing by ttl check. TTL for spoffed IP and legitmate IP will be different.
6. Then return traffic to INPUT chain.
7. Check if the current ip has already 3 connections. If yes drop any additional packet in our case syn packet. Which is the initial packet for any TCP connection.
8. Limit per minute connections irrespective of IP address to 3 with limit burst of 1.