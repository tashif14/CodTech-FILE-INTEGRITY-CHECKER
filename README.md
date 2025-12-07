File Integrity Checker – Improved Brief Documentation
1. Introduction

The File Integrity Checker is a Python-based cybersecurity tool designed to ensure the integrity of critical files. It works by generating and monitoring SHA-256 hash values to detect any unauthorized modifications. This tool is widely applicable in security environments for identifying tampering, detecting malware activity, ensuring configuration integrity, and supporting compliance requirements.

2. Objective

The objective of this project is to build a lightweight yet effective file integrity monitoring solution using Python’s hashlib library.
The tool continuously checks selected files, compares their current hash values with previously stored values, and alerts the user whenever a change is detected.

3. How the Tool Works

The File Integrity Checker follows a straightforward process:

Step 1: Initial Hash Creation

The script calculates an initial SHA-256 hash for every file listed in files_to_monitor.

These hashes are stored in a JSON file (file_hashes.json) for future comparison.

Step 2: Continuous Monitoring

At regular intervals (default: 5 seconds), the script recalculates each file’s hash.

The new hash value is compared with the stored value.

Step 3: Alerts and Detection

The tool provides clear alerts:

Event	Alert Message
File modified	[ALERT] File modified: filename
File missing	[WARNING] File missing: filename
No change	[OK] No change detected
Step 4: Updating Hash Values

If a file modification is detected, the tool automatically updates the new hash in file_hashes.json, ensuring accurate monitoring for subsequent checks.

4. Key Features

✔ SHA-256 hashing for strong integrity verification

✔ Modification detection for monitored files

✔ Missing file alerts

✔ JSON-based hash storage

✔ Customizable monitoring list and interval

✔ Lightweight and easy to deploy

5. Files Included
File	Description
file_integrity_checker.py	Main script responsible for hashing and monitoring
file_hashes.json	Auto-generated hash storage file
6. How to Use the Tool
1. Configure File Monitoring

Edit this section in the script:

files_to_monitor = [
    "test1.txt",
    "test2.txt"
]

2. Run the Script
python file_integrity_checker.py

3. Trigger a Change

Modify one of the files:

echo "New content" >> test1.txt


Expected Output:

[ALERT] File modified: test1.txt
Old hash: d7a9...
New hash: 33f1...

7. Technology Used

Python 3

hashlib – SHA-256 hashing

json – Hash storage database

os, time – File checks and monitoring schedule

8. Limitations

❗ Does not automatically monitor subdirectories

❗ No real-time event-driven detection

❗ No built-in email/SMS alerting

❗ Performance depends on interval settings for large file sets

9. Possible Enhancements

To extend functionality and improve production use:

🔹 Integrate watchdog for real-time monitoring

🔹 Add recursive directory monitoring

🔹 Implement email/SMS alerts for critical file changes

🔹 Send logs to SIEM tools (Splunk, ELK, Azure Sentinel)

🔹 Add GUI dashboard for real-time visibility

🔹 Use HMAC or digital signatures for tamper-proof hash files

10. Conclusion

The File Integrity Checker is an effective and easy-to-use tool for monitoring the integrity of important files. By leveraging SHA-256 hashing, automated monitoring, and alert generation, it provides a foundational level of security suitable for educational purposes, small deployments, and further enhancement in enterprise environments.
This project demonstrates essential cybersecurity practices, including hashing, integrity verification, automation, and secure monitoring.
