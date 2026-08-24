# linux-security-log-analysis

Project Overview

This project demonstrates Linux security log monitoring and authentication- event investigation using Kali Linux. 

The lab  focuses on reviewing system logs, identifying authentication activity, detecting failed and successful login attempts,  monitoring privileged sudo activity, and analyzing SSH authentication events. 

The project follows a SOC-style workflow in which security events are generated in a controlled lab environment, identified in Linux logs, filtered using command-line tools, and analyzed for security relevance.

Objectives

- Identify Linux system and security log sources.
- Analyze authentication-related events.
- Detect failed authentication attempts.
- Identify successful privileged sessions.
- Monitor commands executed with sudo.
- Review SSH service activity.
- Detect successful and failed SSH authentication.
- Identify repeated failed SSH login attempts.
- Correlate successful and failed SSH authentication events.

Lab Environment

- OS: Kali Linux
- Log Analysis Tool: journalctl
- Remote Access Service: OpenSSH
- Shell Utilities: grep, wc,systemctl

Security Relevance

Linux authentication and system logs provide important evidence for identifying unauthorized access attempts, privilege misuse, account compromise, and suspicious remote-login behavior. 

SOC analysts commonly review authentication logs to distinguish normal activity from potentially malicious patterns such as repeated login failures or unexpected privileged access. 

Skills Demonstrated 

-  Linux log analysis
-  Security event investigation
-  Authentication monitoring
-  PAM log analysis
-  SSH log analysis
-  Failed login detection
-  Successful login analysis
-  Privileged command monitoring
-  Log filtering with grep
-  Event counting 
-  SOC investigation methodology

Disclaimer

All activity in this project was performed in a controlled lab environment on systems owned and authorized by the researcher. The generated authentication events were created solely for cybersecurity learning and defensive security analysis.
