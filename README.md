# NETWORKWALKS-B083-WEEK-4-CYBERSECURITY-PENETRATION-TESTING
# Mediroza General Hospital — Black-Box Penetration Test (Training Lab)
Type: Black-box web application penetration test Duration: 5 days Status: Completed — authorized training engagement (Networkwalks, Batch B083)

⚠️ This repository documents a penetration test performed against a lab/training target provided under written authorization as part of a cybersecurity training program. No techniques described here were, or should be, applied to any system without explicit written permission from its owner.

## Overview
This engagement simulated a real-world black-box assessment of a hospital web application, with the goal of identifying vulnerabilities that could expose confidential patient data and sensitive internal business records.

The assessment was scoped to the target domain only, with no social engineering or denial-of-service testing permitted.

## Methodology
1. Reconnaissance — passive and active recon on the target domain, including subdomain enumeration and content/directory discovery.
2. Authentication & Access Control Analysis — mapped login flows and session handling to identify weaknesses in how the app enforces authorization.
3. Exploitation — validated findings with proof-of-concept requests to demonstrate real-world impact (no destructive actions taken).
4. Post-Exploitation Analysis — reviewed retrieved artifacts for secondary exposures (metadata, embedded data).
5. Reporting — findings rated and documented with remediation guidance.

## Key Findings (Summary)
#	Finding __	Category __	Risk
1	Patient lab report portal allowed retrieval of password-protected PDF reports belonging to other patients __	Broken Access Control (OWASP A01:2021) __	High
2	Retrieved PDF reports were protected with weak, dictionary-crackable passwords (cracked via hash extraction + dictionary attack) __	Weak Cryptographic Protection __	Medium
3	An unsecured /old/ directory on the webserver exposed a legacy SQL database backup (mediroza_db_backup_2019.sql) containing full staff salary and personal data	__ Sensitive Data Exposure / Security Misconfiguration (OWASP A05:2021) __ Critical


Screenshots in folder are evidence captured during an authorized training engagement against a purpose-built lab target. Specific patient/staff identifiers shown are synthetic lab data generated for this exercise. 

## Evidence
M1 — Initial Access screenshots/m1-initial-access/01-patient-portal-lab-reports.png Patient portal exposing downloadable, password-protected lab report PDFs.

M2 — Data Extraction (Password Cracking) screenshots/m2-data-extraction/

01-pdf-cracker-match-password.png, 02-pdf-cracker-match-123456.png, 03-pdf-cracker-match-special-char-hash.png — dictionary attack recovering each PDF's password from its extracted $pdf$ hash.
04-patient-report-1-decrypted.png through 06-patient-report-3-decrypted.png — the three decrypted pathology reports, confirming successful recovery.

M3 — Secondary Data Exposure screenshots/m3-data-exposure/

01-old-directory-index.png — directory listing exposing a legacy /old/ path on the webserver.
02-sql-backup-staff-table.png — contents of the exposed SQL backup, including the staff table schema and records (names, job titles, national ID numbers, and salaries).

## Remediation Recommendations
1. Enforce server-side authorization checks on every object reference; never rely on IDs being "hard to guess."
2. Use indirect reference maps or UUIDs instead of sequential/predictable IDs for anything tied to patient records.
3. Apply strong, randomly generated encryption passwords/keys to any documents containing PHI, never user- or pattern-derived passwords.
4. Strip metadata from documents before they are made available for download, and audit file storage locations for unintended public exposure.
5. Apply least-privilege access to any internal HR/finance documents and ensure they are never reachable from the same storage path as patient-facing content.

## Pentest Report
[Mediroza_Pentest_Report.docx](https://github.com/user-attachments/files/32981764/Mediroza_Pentest_Report.docx)


# 👨‍🦰 Author
### Chidozie Zoe Gospel
Cybersecurity Professional B083

LinkedIn: https://www.linkedin.com/in/chidozie-gospel/
