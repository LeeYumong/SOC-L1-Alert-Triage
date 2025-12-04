# SOC-L1-Alert-Triage
This repository demonstrates findings and my hands‑on process for triaging SIEM alerts (inspired by the TryHackMe SOC L1 Alert Triage room). It mirrors the structure and deliverables to show real life scenarios for alerts, investigations, and documentations used by SOC Analysts.

**Objectives:**
- Receive & Categorize Alerts
  - Investigate Logs, EDR, and Network
    - Document, Escalate, and close Alerts
_____________________________________________________________________________________________________________________________________
<img width="1580" height="742" alt="image" src="https://github.com/user-attachments/assets/fd177f83-dc54-4c79-b9d5-a5b0840b3627" />
______________________________________________________________________________________________________________________

Down Below are the Procedures taken to successfully complete this Lab.

**Reviewing the Alert Queues**
- Severity of Alerts (Critical, High, Medium, and Low)
  - Status of Alerts (Awaiting, Action, Closed, etc)
    - Assign the correct roles
      - Verdict (True/False Positive)
 
 **Prioritize Alerts by Severity** 
- Critical
  - High
    - Medium
      - Low
_____________________________________________________________________________________________________________________________________
<img width="1535" height="712" alt="image" src="https://github.com/user-attachments/assets/cb2c4489-a47c-404e-b538-75636d1fa074" />
______________________________________________________________________________________________________________________

**Assign Highest-Priority Alert**
- To prevent multiple anaylst from working/operating the same Alert
  - Prove ownership of the Alert

**Change Alert to "In Progress"**
- Shows what Alerts are being worked on and what is not.

**Write a brief summary of the Investigation and what was found for future similar Scenarios**

**Begin Investigation (MetaData --> Evidence --> Logs)**

**1st Scenario**
_____________________________________________________________________________________________________________________________________
<img width="1510" height="426" alt="image" src="https://github.com/user-attachments/assets/10db74bd-23d5-437f-9eea-071ac042db61" />
______________________________________________________________________________________________________________________

**Alert Name:** Potential Data Exfiltration

**Time:** March 21, 2025 / 13:30 

**Severity:** Critical

**Status:** In Progress

**Host/Source:** 
- Source IP: 192.168.45.66 
  - Host: UK04/MEETINGROOM

**Process Name:** TBD (To Be Determined)

**Trigger:** Rule triggered by **>5 GB data** sent to a single destination within **24hrs**.

**Description:** 
- Destination: *.zoom.us (Most likely Zoom).
  - Data Volume: 5.8 GB sent / 5.2 GB received.
    - Possible sensitive data exposure.
      - Confirm legitimate business use and user responsible.

**Actions to be Taken:**
- Temporarily isolate or monitor host.
  - Cross-reference with DLP policies.
    - Verify Zoom logs for timeframe.
      - Escalate to IT Security Manager if abnormal activity confirmed.

**Procedures Taken:**
- Validated if the destination is legitimate.
  - Identified the host and its purpose.
    - Checked User Actions.
      - Pulled Zoom Activity Logs.
        - Access Data Sensitivity.
          - Compared Data Volume to typical Zoom Usage.
            - Check for other unusual Outbound Traffic.

**Verdict:** False Positive

**Status:** Closed

**Probable Cause of High Data Volume:**
- Sharing Multiple Large Files.
  - High-Resolution Screen Sharing/Video Streaming (720p/1080p).
    - Long Meeting Durations/Large Participants.
      - Cloud Recording.

**Comments:**
- Confirmed the Zoom Meeting is an authorized/legitimate business meeting. 
  - High Data Volume was caused due to a large amount of Participant using High-Resolution Screen Sharing with multiple participant video feed during a prolonged meeting.
    
_____________________________________________________________________________________________________________________________________
<img width="1473" height="693" alt="image" src="https://github.com/user-attachments/assets/9aacdcac-079e-4921-94f6-81c5ad4ce4e4" />
______________________________________________________________________________________________________________________

**2nd Scenario:**
_____________________________________________________________________________________________________________________________________
<img width="1495" height="373" alt="image" src="https://github.com/user-attachments/assets/a21ff2ad-6494-4a08-a964-33596b4605a8" />
______________________________________________________________________________________________________________________

**Alert Name:** Double-Extension File Creation

**Time:** March 21, 2025 / 13:58

**Severity:** High

**Status:** In Progress

**Host/Source:** Host: LPT-HR-009

**Process Name:** 
- Process: chrome.exe
  - Process User: S.Conway

**Trigger:** Detection of double-extension file (*.mp4.exe)

**Description:**
- Target File: C:\Users\S.Conway\Downloads\cats2025.mp4.exe
  - MotW URL: https://freecatvideoshd.monster/cats2025.mp4.exe
    - MD5: 14d8486f3f63875ef93cfd240c5dc10b
      - Mimics benign video but executable
        - Downloaded from untrusted domain, potential malware/phishing

**Actions to be Taken:**
- Ensure the File is Not Executed.
  - Contain the Risk.
    - Gather Information About the File.
      - Investigate the Source URL/Domain.
        - Examine the File Safely.
          - Gather Endpoint Context before Execution.
         - Monitor Network Logs before Executions.
      - Prepare a Safe Environment for Analysis.
    - Verify User's Activity.
  - Assess whether to Escalate if needed before proceeding further.

**Procedures Taken:**
- Validate whether the File Executed.
  - Perform Hash Reputation Lookup.
    - Analyze the Download Source.
      - Perform Static Analysis.
    - Search Environment for further Spread.
  - Interview User how the file was downloaded.
- Apply Blocking Measures. 

**Verdict:** True Positive

**Status:** Closed

**Comment:**
- File was downloaded, but not executed.
  - User reported it originated from a prize-winning phishing email.
    - No malicious process observed.
      - File quarantined and URL/hash submitted for IOC monitoring.
_____________________________________________________________________________________________________________________________________
<img width="1468" height="610" alt="image" src="https://github.com/user-attachments/assets/6b98167a-6e89-4eae-a80e-8ee90c15e3aa" />
______________________________________________________________________________________________________________________


