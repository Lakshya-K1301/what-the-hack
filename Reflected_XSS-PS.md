Reflected XSS — Reflected XSS into HTML context with nothing encoded

Date: 25 Sept 2026  Source: PortSwigger Web Academy — [Reflected XSS into HTML context with nothing encoded]

Vulnerability Class

Reflected Cross-Site Scripting (XSS)

Target / Context

Search Bar at the home page of the application, the search term is sent to the server and reflected back to the user in the url and on the page without valdiation or encoding.

Mechanism

If a app has not properly setup input validation and output encoding on fields that take input from the user to construct the output of the page after processing it like search bars then the attacker can use it to their advantage by inputting a malicious script inside the search bar and if unproper url encoding is present then the attacker can easily share that link to victims in various way and as soon as they visit that site the malicious script is reflected back and it executes leading to the user's sensitive data and privleges being shared to the attacker 

Payload

<script>alert('XSS by Prometheus')</script>

Root Cause

The root cause is not having proper output encoding and minor causes are not having proper input validation and url encoding

Why It Worked

It worked because the app didn't had any proper output encoding because of which when the attacker entered the malicious script <script>alert('XSS by Prometheus')</script> it went to the server which processed it as any other search request and built the output page with the script in it and when it load the script  executes leading to an reflected XSS attack

Detection Note (Defender's Lens)

Proper logging of incoming resquests and outgoing responses is required at transit so that malicious activity can be detected 
Setup of automatic XSS detectors and Firewalls like WAF is required as they automatically check the input for unnecceray or malicious search request and looking for specific keywords like <script> or onerror=
they also perform automatic tests by sending a harmless ?search=xssTest7f3a2 and then looking the response for that specific string if its found then the site is reflecting if it is not found or an encoded version of it is found then it is not reflecting and the site is not reflecting

Remediation

setup proper output and URL encoding and input validation will help too, also setting up automatic XSS detectors and WAF will also help