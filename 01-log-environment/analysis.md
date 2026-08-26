Linux Log Environment

Objective:

Identify the Linux operating system environment and locate the system log directory used for security and system-event investigation.

Commands Used: 

- whoami
- cat /etc/os-release
- ls /var/log

Log Source: 

Linux stores many traditional system and security logs under: /var/log/

Depending on the Linux distribution and logging configuration, security events may also be recorded in the systemd journal and accessed using journalctl.

Analysis:

The /var/log/ directory contained multiple log files and directories that can provide information about system activity, authentication events, login history, services and other operating-system events.

The system also uses the systemd journal, which allows security-related events to be queried and filtered using journalctl.

Observation:

Linux provides multiple sources of security-relevant information. Traditional log files under /var/log and events stored in the systemd journal can be used together during security investigations.

Security Relevance:

Idenitfying available log sources is an important is an imporatant fisrt step in host-based security monitoring. SOC analysts need to unnderstand where authentication, system, service and security events are recorded before investigating suspicious acitivty. 

Key Learning: 

- Identified the primary Linux log directory.
- Reviewed available system log sources.
- Learned the role of /var/log in Linux monitoring.
- Identified journalctl as a method for accessing systemd journal events.
- Established the log sources that will be used in later authentication investigations.