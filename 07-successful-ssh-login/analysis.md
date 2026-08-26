Successful SSH Login Investigation

Objective:

Generate a controlled successful SSH login and investigate the resulting authentication events in the linux system journal. 

Test Scenario: 

An SSH connection was initiated to the Kali Linux system in the controlled lab environment.

The correct account credentials were provided, resulting in a successful SSH authentication and the creation of a remote user session.

After terminating the SSH session, the SSH service logs were reviewed for evidence of the successful authentication.

Command Used: 

sudo journalctl -u ssh --since "10 minutes ago"

Log Source: 

The investigation queried events associated specifically with the SSH service using: -u ssh

The --since "10 minutes ago" option restricted the results to recent activity, reducing unrelated historical events.

Analysis:

The SSH service logs contained an authentication event showing that the supplied credentials were successfully accepted.

The relevant event contained:

Accepted password for USER from 192.168.x.x port 54828 ssh2

A corresponding PAM event showed that an SSH session was subsequently opened:

pam_unix(sshd:session): session opened for user USER

Together, these events confirm that authentication succeeded and an SSH session was established.

The logs provided several useful pieces of information, including the account involved, source address, source port, authentication result, SSH protocol, and session status.

Observation: 

The SSH logs provided evidence of both successful authentication and subsequent session creation.

Important fields identified included:
- Timestamp — when the authentication occurred
- sshd — service responsible for processing the connection
- Accepted password — successful authentication result
- Username — account that authenticated
- Source IP — system initiating the connection
- Source port — client-side connection port
- ssh2 — SSH protocol
- session opened — confirmation that a user session was established

Security Relevance:

Successful SSH authentication events should be monitored because successful access does not necessarily mean authorized access.

During a real investigation, an analyst could compare the username, source address, timestamp, and authentication method against expected user behavior.

A successful SSH login that occurs after repeated failed authentication attempts, originates from an unexpected source, or involves an unusual account may require additional investigation.

Finding:

Event Type: Successful remote authentication
Service: SSH / sshd
Authentication Method: Password
Account: Lab user
Source: Private lab host (192.168.x.x)
Protocol: SSH2
Result: Authentication accepted and session opened
Severity: Informational in this controlled lab scenario
Action: Correlate with source, user, failed attempts, and subsequent activity

Key Learning: 

- Generated a successful SSH authentication event.
- Queried service-specific logs using journalctl -u ssh.
- Identified the Accepted password SSH event.
- Identified the corresponding PAM session-opening event.
- Extracted the username, source address, source port, protocol, and authentication result from an SSH log.
- Learned why successful remote authentications should be correlated with other security events.
