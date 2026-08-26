Repeated Failed SSH Authentication Analysis

Objective:

Analyzed repeated failed SSH authentication events within a defined time window and count the number of failures observed. 

Investigation Scenario:

Two failed SSH password attempts had previously been generated in the controlled Kali Linux lab.

Instead of examining each event individually, the SSH logs were analyzed within a 30-minute window to determine how many failed authentication attempts had occurred.

This demonstrates a basic method for identifying repeated authentication activity.

Command Used:

First, the failed SSH authentication events were displayed: sudo journalctl -u ssh --since "30 minutes ago" | grep "Failed password"

The number of failed authentication events was then counted: sudo journalctl -u ssh --since "30 minutes ago" | grep "Failed password" | wc -l

Log Source: 

SSH service events were retrieved from the systemd journal using: journalctl -u ssh

The investigation used three stages of filtering: 
--since "30 minutes ago" > grep "Failed password" > wc -l 

This restricted the investigation to recent SSH activity, selected failed password events, and counted the resulting entries.

Analysis:

The SSH logs contained two failed password authentication events within the selected 30-minute period.

The individual events contained information similar to:
Failed password for USER from 192.168.x.x port 47650 ssh2

The counting command returned:
2

This confirmed that two failed SSH authentication events occurred within the investigated time window.

Both events were generated intentionally in the controlled lab and therefore do not represent an actual brute-force attack.

Observation:

The analysis demonstrated that Linux command-line utilities can be combined to move from individual log-event identification to basic event aggregation.

Security Relevance: 

A failure count alone is not sufficient to confirm malicious activity. Analysts should correlate the events with source IP addresses, targeted accounts, timestamps, successful authentications, and other security telemetry.

Finding:

Event Type: Repeated failed SSH authentication
Service: SSH / sshd
Time Window: 30 minutes
Failed Events Observed: 2
Source: Private lab host (192.168.x.x)
Result: Repeated authentication failures identified
Assessment: Controlled lab activity; not classified as a brute-force attack
Action: Correlate with successful SSH authentication and source information

Key Learning: 

- Defined a time window for SSH log analysis.
- Filtered logs specifically for failed password events.
- Used wc -l to count matching security events.
- Identified repeated authentication failures from log data.
- Learned the difference between detecting repeated failures and declaring a brute-force attack.
- Practiced basic event aggregation using Linux command-line tools.
- Applied a SOC-style approach to authentication-pattern analysis.