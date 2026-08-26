Failed Authentication Investigation

Objective:

Generate a controlled failed authentication attempt and investigate the resulting Linux security event using the system journal.

Test Scenario:

A failed authentication event was intentionally generated in the controlled Kali Linux lab by attempting to  execute a command with sudo and providing an incorrect password.

This activity was performed only to genearte security-log evidence for analysis. 

Command Used: 

sudo journalctl --since "10 minutes ago" | grep -i "authentication failure"

Log Source:

The authentication event was retrieved from the systemd journal using journalctl.

The results were filtered for: authentication failure 

A 10 minute time window was used to reduce unrelated historical events and focus the investigation on the recently generated authentication attempt.  

Analysis:

The filtered journal identified a PAM authentication failure associated with sudo.

The relevant event contained: pam_unix(sudo:auth): authentication failure

The log also provided contextual information including the user ID, effective user ID, terminal,  requesting user, and account associated with the authentication attempt. 

This confirmed that the unsuccessful authntication attempt generated a secuirty-relevant event that could be identified through Linux  log analysis. 

Observation:

A failed sudo authentication attempt was successfully identified in the linux system journal. 

The event contained information that could help an analyst determine: 
- When the authenitcation failure occured
- Which authentication mechanism generated the event
- Which user initiated the request
- Which terminal was involved
- Whether authentication succeeded or failed

Security Relevance:

Failed authentication events are important indicators during security monitoring.

An isolated failure may result from an incorrectly enetered password. However, repated authentication failures within a short period may indicate password guessing, unauthorized access attempts, or other suspicious authentication activity. 

Finding:

Event type- Failed privileged authentication
Authentication Mechanism- sudo
Result- Authetication Failure
Severity- Informational in this controlled single event scenario
Action- Review for repeated failures or related suspicious activity

Key Learning: 

- Generated a controlled authentication failure.
- Located the resulting event in the Linux system journal.
- Filtered logs using a specific time window and event keyword.
- Identified a PAM sudo authentication failure.
- Distinguished a single failed authentication event from a pattern that could indicate suspicious activity.
- Practiced a basic SOC workflow of event generation, detection, filtering, and analysis.