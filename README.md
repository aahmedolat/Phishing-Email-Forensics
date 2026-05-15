## Phishing Email Forensic Simulation Report

### 1. Executive Summary

A suspicious email received through the company email system was analyzed using email header analysis, URL inspection, and threat intelligence tools. The investigation identified suspicious links commonly used in phishing attacks.

One shortened URL redirected users to another external website that was flagged by multiple security vendors as phishing and malicious. Additional indicators, including missing DMARC protection and mismatched email routing information, further confirmed suspicious activity.

Based on the findings, the email is assessed as a phishing attempt intended to trick users into clicking malicious links.

![Email Body]()

### 2. Email Body URL and Attachment Analysis

#### a) Embedded Suspicious URLs

Two URLs were identified in the email:

* `http://bit.ly/3IR0iq3?575504`

  * Redirected to:
  * `https://ripple.com.gt/insights/staking-program/`

* `https://eportfolioapp.nl/?plbms406qayn72wwk3r6cxxc0xc0svab`

The URLs were analyzed using:

* URLScan.io
* VirusTotal

![Email Body Link]()

#### b) Threat Intelligence Results

**URLScan.io Findings**

* No malicious classification was detected for the Bit.ly URL.
* The shortened URL acted as a redirect link, which is commonly used by threat actors to hide the final destination.

![URLScan]()

**VirusTotal Findings**

![VirusTotal-1]()
![VirusTotal-2]()

* The Bit.ly redirect URL was flagged by multiple security vendors as:

  * Phishing
  * Malicious
  * Malware-related

* The redirected final URL was also flagged by security vendors as phishing.

![VirusTota1-3]()

* The second URL shared the same domain as the sender’s email address (`eportfolioapp.nl`).

* No vendors flagged this domain as malicious, but its use in the email remains suspicious.

![VirusTotal-4]()

#### c) Attachment Analysis

No attachment was included in the email; therefore, no attachment analysis was performed.

### 3. Email Header Analysis

Further analysis was performed on the email header to identify additional phishing indicators.

#### a) Sender Information

* Sender IP Address: `167.89.89.163`
* Sender Email Address: `Binance <noreply@eportfolioapp.nl>`
* SPF: Pass
* DKIM: Pass
* DMARC: None
* SMTP Server: `sendgrid.net`
* Return-Path: `@sendgrid.net`

The email was sent using SendGrid mail infrastructure.

![EmailHeader-1]()

#### b) IP Reputation Check

**VirusTotal / WHOIS Results**

* The IP address belongs to SendGrid.
* No major security vendor flagged the IP as malicious.

![VirusTotal-IP]()

**AbuseIPDB Results**

* The IP address was previously reported for spam and phishing-related activity.
* This indicates the IP may have been used in previous phishing campaigns.

![AbuseIPDB]()

#### c) Email Authentication Results

**SPF (Sender Policy Framework): PASS**

* The sending server was authorized to send emails on behalf of the domain.
* However, SPF alone does not confirm the email is safe.

**DKIM (DomainKeys Identified Mail): PASS**

* The email contained a valid DKIM signature.
* This confirms the message was signed by the sending domain.

**DMARC (Domain-based Message Authentication, Reporting, and Conformance): NONE**

* No DMARC policy was configured for the domain.
* This increases the risk of spoofed or unauthorized emails.

#### d) Send and Return Path Analysis

The email showed inconsistencies between:

* Sender email address
* Sending server
* Return-Path information

These mismatches are common indicators of phishing emails.

![EmailHeader-2]()

### 4. Indicators of Compromise (IoCs)

* Suspicious embedded URLs
* Redirect links hiding the final destination
* Missing DMARC protection
* Mismatched sender and return-path information
* Previously reported phishing-related IP activity

### 5. Conclusion

The email is confirmed to be a phishing attempt. The message used suspicious redirect links, hidden destinations, and unusual email routing behavior commonly seen in phishing attacks.

Threat intelligence scans identified the embedded URLs as phishing and malicious. Although SPF and DKIM checks passed, the lack of DMARC protection and suspicious routing information increased the likelihood of malicious intent.

### 6. Recommendations

1. Remove and quarantine the email from all user inboxes.
2. Block the identified malicious URLs and related domains on firewalls, proxies, DNS filters, and email gateways.
3. Monitor logs and endpoint activity to identify users who may have clicked the links.
4. Strengthen email security by enforcing DMARC policies in addition to SPF and DKIM validation.
5. Conduct phishing awareness training for employees.
6. Report the phishing indicators to Microsoft Security, APWG, and Google Safe Browsing.
7. Continue monitoring for similar phishing emails using related domains or infrastructure.

### Prepared by:
**Ahmed Olatunji** - Cybersecurity Analyst
