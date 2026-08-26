Failed SSH Login Detection

Objective:

Generate controlled failed SSH authentication attempts identifying the resulting security events in the Linux SSH service logs.  

Test Scenario:

SSH connection was initiated to the Kali Linux system in the controlled lab environment. 

Incorrect credentials were delibrately entered twice to generate failed ssh authentication event. 

The SSH service logs were then examined to determined whether the failed login attempts had been recorded. 

Command Used:

sudo journalctl -u ssh --since "10 minutes ago" | grep "Failed password"

Log Source: 

SSH servicce events were retrieved from the systemd journal using: journalctl -u ssh

The results were filtered using: grep "Failed password"

Analysis:

The filtered SSH logs identified two failed password authentication attempts. 
Failed password for USER from 192.168.x.x port 47650 ssh2

The Failed password status confirms that the SSH server rejected the supplied credentials.

The events also provided useful investigation detals including the account targeted, source IP address, source port, timestamp, SSH service, and protocol. 

As the attempts were intentionally generated as part of this controlled lab, they do not represent a  real attack. 

Observation: 

Two failed SSH authetication events were successfully identified. 

Important fields included-
- Time stamp- when each attempt occurred
- sshd- service processing the authentication
- Failed password- authetication result
- Username- account involved in the attempt
- Source IP- system initiating the connection 
- Source port- client-side connection port
- ssh2- SSH protocol

Multiple failed events from the same source can be grouped and investigated as related authentication activity.

Security Relevance: 

Failed SSH authentication events are important indicators for security monitoring.

A small number of failures may result from legitimate users entering incorrect credentials. However, a high number of repeated failures against one or more accounts within a short period may indicate password guessing or brute-force activity.

Finding:

Event Type: Failed remote authentication
Service: SSH / sshd
Authentication Method: Password
Account: Lab user
Source: Private lab host (192.168.x.x)
Failed Attempts Observed: 2
Protocol: SSH2
Result: Authentication rejected
Severity: Informational in this controlled lab scenario
Action: Check for repeated failures and subsequent successful authentication

Key Learning: 

- Generated controlled failed SSH authentication events.
- Filtered SSH logs for Failed password events.
- Identified multiple failed login attempts.
- Extracted the username, source IP, source port, and authentication result.
- Learned how repeated authentication failures can form the basis of a brute-force investigation.
- Distinguished failed SSH authentication from the successful SSH event investigated previously.