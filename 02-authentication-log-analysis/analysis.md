Authentication Log Analysis

Objective:

Review Linux system logs to identify authentication, session and privileged access events that may be relevant to a security investigation. 

Command Used:

sudo journalctl | grep -i  "authentication\|session\|sudo" |tail -n 15 

Log Source: 

The investigation used the systemd journal, accessed through: journalctl

The output was filtered using grep to  identify events containing authentication, session or sudo information. 

Analysis: 

The Linux system journal was reviewed for authentication-related activity. Filtering the journal reduced the amount of unrelated system information and highlighted events associated with user sessions and privileged access.

The results included PAM and sudo session events, including entries showing privileged sessions being opened and closed.

Observation: 

The filtered journal contained security-relevant events associated with authentication and privileged sessions.

The logs provided information such as:

- Timestamp of the event
- Authentication/session mechanism
- User context
- Privileged account
- Session status

Filtering the journal makes it easier to isolate relevant authentication activity from general operating-system events.

Security Relevance: 

Authentication logs are important for detecting unauthorized access attempts, unusual login behavior, privilege misuse, and potentially compromised accounts.

SOC analysts can use these events as a starting point for further investigation and correlate them with failed logins, successful logins, SSH activity, and privileged commands.

Key Learning: 

- Used journalctl to review Linux system events.
- Used grep to filter security-relevant log entries.
- Identified PAM authentication/session events.
- Identified sudo privileged-session activity.
- Learned how log filtering helps reduce unrelated system events during an investigation.