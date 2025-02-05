#  SOC287 - Arbitrary File Read on Checkpoint Security Gateway CVE-2024-24919

## Overview
This repository contains a detailed walkthrough of the CVE-2024-24919 vulnerability affecting Check Point Security Gateways. The vulnerability allows arbitrary file read, potentially exposing sensitive system files such as /etc/passwd. This write-up provides an in-depth analysis of the attack scenario, detection methods, and mitigation strategies.

## Lab Walkthrough
For a detailed walkthrough of this Let's Defend SOC lab, please refer to:
[SOC287 Lab Walkthrough]([SOC287 Lab Walkthrough](SOC287%20-%20Arbitrary%20File%20Read%20on%20Checkpoint%20Securit%2054f2405b780549d3a338990c29c20f1f.md)
)

## Overview
- CVE ID: CVE-2024-24919
- Vulnerability Type: Arbitrary File Read
- Affected System: Check Point Security Gateways
- Exploit Method: Directory Traversal
- Severity: High

## Attack Scenario
In this incident, an attacker exploited CVE-2024-24919 to send a directory traversal payload via an HTTP POST request to access the /etc/passwd file on the target. Below are the key details from the alert:

- Event Time: June 6, 2024, 03:12 PM
- Target System: 172.16.20.146 (Internal Check Point Gateway)
- Source IP: 203.160.68.12
- requested URL: 172.16.20.146/clients/MyCRL
- Payload: aCSHELL/../../../../../../../../../../etc/passwd
- User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:126.0) Gecko/20100101 Firefox/126.0
