# CodTech-FILE-INTEGRITY-CHECKER

File Integrity Checker – Documentation
1. Introduction

The File Integrity Checker is a Python-based security tool designed to detect unauthorized modifications to files by calculating and comparing their cryptographic hash values over time. It helps ensure file integrity, identify tampering, and support security monitoring processes.

This tool is useful in cybersecurity for:

Detecting unauthorized changes

Monitoring configuration or log files

Identifying malware activity

Maintaining compliance and audit readiness

2. Objective

The objective of this task is to build a simple but effective file integrity monitoring tool using Python’s hashlib library.
The script calculates the SHA-256 hash of each monitored file and alerts the user if a file’s content has been altered, deleted, or replaced.

3. How the Tool Works

The program performs the following steps:

Step 1 — Initial Hash Generation

The script computes SHA-256 hashes for each file listed in files_to_monitor.

These hashes are stored in a JSON file named file_hashes.json.

Step 2 — Continuous Monitoring

The script repeatedly recalculates the hash values at a defined interval (default: every 5 seconds).

Each new hash is compared with the stored hash.

Step 3 — Alerts

The tool generates different alerts:

Event	Alert
File modified	[ALERT] File modified: filename
File missing	[WARNING] File missing: filename
No change	[OK] No change detected
Step 4 — Hash Update

When a file change is detected, the hash value in file_hashes.json is updated automatically.

4. Features

✔ Calculates SHA-256 hashes
✔ Detects file modification
✔ Detects missing / deleted files
✔ Stores and loads hash values in a JSON file
✔ Easy to configure and extend
✔ Lightweight and suitable for security monitoring tasks

5. Files Included
File Name	Description
file_integrity_checker.py	Main Python monitoring script
file_hashes.json	Stores the hash values of monitored files (auto-generated)
6. How to Use the Tool
1. Modify the file list

In the __main__ block, list the files you want to monitor:

files_to_monitor = [
    "test1.txt",
    "test2.txt"
]

2. Run the script
python file_integrity_checker.py

3. Modify a file to test
echo "New content" >> test1.txt


You will see:

[ALERT] File modified: test1.txt
Old hash: d7a9...
New hash: 33f1...

7. Technology Used

Python 3

hashlib for SHA-256 hashing

json for storing hash records

os, time for file checking and monitoring intervals

8. Limitations

⚠ Does not monitor subdirectories
⚠ No real-time OS-level events (uses time-based polling)
⚠ No alert notifications (email/SMS) — can be added

9. Possible Enhancements

You can extend this tool further by adding:

🔹 Real-time monitoring using watchdog
🔹 Directory-wide monitoring
🔹 Email or SMS notifications
🔹 Log integration (Syslog, SIEM/Splunk)
🔹 GUI dashboard
🔹 Tamper-proof hash storage

10. Conclusion

This File Integrity Checker provides a simple but effective way to monitor file changes using SHA-256 hashing. It demonstrates essential cybersecurity concepts such as integrity verification, hashing, alerting, and monitoring automation. The tool serves as a strong foundation for more advanced file integrity monitoring systems used in enterprise security.
