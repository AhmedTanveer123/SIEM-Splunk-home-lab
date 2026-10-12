# SIEM-Splunk-home-lab
SOC Analyst Home Lab: SMB Activity Detection with Splunk

Project Overview

This project demonstrates a home lab for monitoring Windows Security logs and investigating Server Message Block (SMB) file-share activity using Splunk Enterprise.

The lab simulates authorized SMB activity from Parrot OS to a Windows 11 machine, then analyzes the resulting security events in Splunk.

Lab Architecture

Data flow:

"Parrot OS → Windows 11 → Splunk Universal Forwarder → Splunk Enterprise"

- Parrot OS: Used to test SMB connectivity and access a shared folder.
- Windows 11: Target machine hosting the "LabShare" network share and generating Security logs.
- Splunk Universal Forwarder: Collects and forwards Windows event logs.
- Splunk Enterprise: Searches the collected logs and supports security detection and alerting.

See ""architecture.png"" (architecture.png).

Tools and Technologies

- Parrot OS
- Windows 11
- SMB / Windows file sharing
- Windows Security Event Logging
- Splunk Universal Forwarder
- Splunk Enterprise
- Search Processing Language (SPL)

Lab Activities

1. Tested SMB connectivity from Parrot OS to Windows 11.
2. Investigated SMB authentication and share access.
3. Created a dedicated Windows network share named "LabShare".
4. Uploaded harmless test files: "soc-test.txt" and "suspicious-test.ps1".
5. Verified that Windows Security events were forwarded to Splunk.
6. Investigated Event ID "5145" for activity associated with the test machine and files.
7. Configured a Splunk alert for matching SMB activity.

Detection and Investigation

Event ID 5145 — Detailed File Share Access Check

Windows recorded events associated with SMB share-access checks.

The investigation identified:

- Source IP: "192.168.205.133"
- Windows hostname: "ANONYMOUS"
- Account observed: "saiko"
- Share: "LabShare"
- Event ID: "5145"

The raw event data was used to investigate references to the test filenames.

See the "queries/" directory for the SPL searches used during the investigation.

Evidence

Screenshots documenting the investigation are available in ""screenshots/"" (screenshots/):

- Windows Security log collection in Splunk
- SMB activity associated with the Parrot IP
- Account and network-share details
- Raw events referencing test filenames
- Splunk alert enabled status

Key Learnings

- Windows Security event collection and forwarding
- SMB network-share investigation
- Searching and filtering Windows events using SPL
- Reviewing raw event data when field extraction is unavailable
- Configuring security alerts in Splunk
- Documenting detection evidence and limitations

Limitations

Event ID 5145 records detailed share-access checks. It does not independently prove that a file was successfully written or that a compromise occurred.

The configured alert was enabled, but its successful triggering must be verified separately. Searches for Event IDs 4624 and 4625 did not return matching events from the Parrot IP during the tested time range.

Conclusion

This project demonstrates an end-to-end security monitoring workflow: generating authorized SMB test activity, collecting Windows Security logs, investigating relevant events in Splunk, and configuring a detection alert.

All activities were performed in a controlled lab environment.
