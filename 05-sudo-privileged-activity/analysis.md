Sudo Privileged Activity Monitoring

Objective:

Monitor commands  executed with elevated privileges and identify sudo activity recorded in Linux security logs. 

Test Scenario:

A harmless privileged command was intentionally executed in the controlled Kali Linux lab: sudo ls /root

Command Used:

sudo journalctl --since "10 minutes ago" | grep "COMMAND="

Log Source:

The investigation used the systemd and journal through journalctl. 

The journal output was filtered for: COMMAND=

This allowed sudo events containing executed command information to be isolated from unrelated system activity.

Analysis: 

The filtered journal showed commands that had been executed using sudo.

The relevant event contained information similar to: USER=root ; COMMAND=/usr/bin/ls/root

The log also recorded contextual information such as the requesting user, terminal, current working directory, target privileged account, and executed command.

This demonstrated that Linux logs can provide evidence not only that privileged access occured, but also what command was executed during that activity. 

Observation:

The sudo event provided sevaeral useful fileds for security analysis:
- User- account that initiated the privileged action
- TTY- terminal associated with command 
- PWD- working directory from which the command was executed
- USER=root- account under which the command was executed 
- COMMAND- command executed with elevated privileges

The test command was successfully recorded as privileged activity in the system journal.

Security Relevance:

Monitoring sudo activity is important because privileged accounts can make significant changes to a Linux system. 

Unexpected or unauthorized privileged commands may indicate account compromise, privilege misuse, or malicious activity.

During an investigation, SOC analysts can correlate sudo command events with authentication activity, usernames, timestamps, processes, and other system events to determine whether privileged activity is expected.

Finding:

Event Type: Privileged command execution
Privilege Mechanism: sudo
Target User: root 
Command Observed:/usr/bin/ls/root
Result: Privileged command executed and logged 
Severity: Informational in this controlled lab scenario
Action: Review privileged commands for unexpected or unauthorized activity

Key Learning:

- Monitored commands executed using sudo.
- Used COMMAND= to isolate privileged command activity.
- Identified the account responsible for initiating a privileged command.
- Identified the command executed with root privileges.
- Learned how Linux logs provide context for privileged-user activity.
- Practiced correlating authentication and post-authentication activity.