SSH Authentication Correlation

Objective: 

Correlate successful and failed SSH authentication events to demonstrate how multiple security events can be reviewed together during an investigation.

Investigation Scenario:

Previous investigations identified both successful and failed SSH password authentication events in the controlled Kali Linux lab.

Rather than examining these events separately, the SSH logs were filtered to display both authentication outcomes together.

This allowed successful and unsuccessful authentication activity to be compared within the same investigation.

Command Used:

sudo journalctl -u ssh --since "30 minutes ago" | grep -E "Accepted password|Failed password"

Log Source:

SSH authentication events were retrieved from the systemd journal using:
journalctl -u ssh

The output was filtered using:
grep -E "Accepted password|Failed password"

The extended regular expression allowed both successful and failed password authentication events to be displayed together.

Analysis:

The filtered SSH logs contained two different authentication outcomes.

A successful authentication event appeared as:
Accepted password for USER from 192.168.x.x port 54828 ssh2

Failed authentication events appeared as:
Failed password for USER from 192.168.x.x port 47650 ssh2

Reviewing both event types together made it possible to compare the account, source address, timestamps, authentication results, and connection information.

In this controlled lab, the successful and failed authentication events were intentionally generated for analysis. Therefore, the presence of both event types does not represent an actual account compromise.

Observation: 

Both accepted and failed SSH password events were successfully isolated from the SSH service logs.

The correlation provided several useful fields:

Timestamp — when each authentication attempt occurred
Authentication result — accepted or failed
Username — account involved
Source IP — origin of the SSH connection
Source port — client-side connection port
Service — sshd
Protocol — SSH2

Comparing these fields allows related authentication events to be examined as part of a wider sequence rather than as isolated log entries.

Security Relevance:

Correlation is an important part of SOC investigations because individual log events may not provide enough context to determine whether activity is suspicious.

For example, repeated failed authentication attempts followed by a successful login from the same source could warrant further investigation.

An analyst could then investigate additional evidence such as:
- Number and frequency of failed attempts
- Source IP address
- Targeted account
- Time between failed and successful authentication
- Commands executed after successful access
- Privilege escalation activity
- Other events associated with the same account or host

However, the sequence alone does not prove that an account was compromised. Additional context and telemetry would be required.

Finding:

Event Category: SSH authentication activity
Service: SSH / sshd
Authentication Method: Password
Events Reviewed: Successful and failed authentication
Source: Private lab host (192.168.x.x)
Result: Authentication events successfully correlated
Assessment: Controlled lab-generated activity
Action: In a production environment, investigate unusual failure-to-success authentication patterns and correlate them with post-login activity

Key Learning: 

- Correlated successful and failed SSH authentication events.
- Used extended grep filtering to identify multiple event types.
- Compared authentication results within a defined time window.
- Identified common fields that can link related authentication events.
- Learned why failed-to-success authentication patterns may require investigation.
- Avoided treating authentication patterns alone as proof of compromise.
- Practiced a basic SOC event-correlation workflow.

Investigation Conclusion:

The SSH investigation demonstrated a progression from service monitoring to authentication-event detection and correlation.

The investigation successfully identified:

- An active SSH service.
- Successful SSH authentication.
- Failed SSH authentication attempts.
- Repeated failed authentication activity.
- Successful and failed events correlated within the SSH logs.

This demonstrates how Linux security logs can be used to investigate remote authentication activity and provide evidence for further SOC analysis.