Successful  Authentication Investigation

Objective:

Generate and identify a successful privileged authentication event in Linux and compare it with the failed authentication activity investigated previously. 

Test Scenario:

A successful privileged session was intentionally generated in the controlled Kali Linux lab by executing a command with sudo and providing the correct user password.

Command Used:

The privileged authentication event was generated using: sudo whoami

The resulting event was investigated using: sudo journalctl --since "10 minutes ago" | grep "session opened for user root"

Log Source:

The results were filtered for: session opened for user root 

This allowed successful privileged-session events to be isolated from unrelated syatem activity.

Analysis:

The journal contained a PAM session event showing that a privileged root session had been successfully opened through sudo. 

unlike the failed authentication event identified in the previous investigation, this event indicates that authentication succeeded and a privileged session was created. 

The event also provides user context that can help determine which account initiated the privileged session. 

Observation:

A successful privileged session was identified in the Linux system journal. 

The log provided information about:
- Event timestamp
- PAM authentication
- Privileged account 
- User ID
- User responsible for initiating the session
- Successful session creation

Finding:

Event Type: Successful privileged session
Authentication Mechanism: PAM / sudo
Target Account: root
Result: Privileged session opened successfully
Severity: Informational in this controlled lab scenario
Action: Correlate with preceding authentication attempts and subsequent privileged activity

Key Learning: 

- Identified a successful privileged Linux session.
- Used journalctl to locate recent authentication events.
- Used grep to isolate successful root session activity.
- Distinguished an authentication failure from a successfully opened session.
- Learned why successful authentication events also require monitoring.
- Practiced correlating authentication events during a security investigation.