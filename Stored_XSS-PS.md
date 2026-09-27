Stored XSS — Stored XSS into HTML context with nothing encoded

Date: 26 Sept,2026  Source: PortSwigger Web Academy — Stored XSS into HTML context with nothing encoded

Vulnerability Class

Stored Cross Site Scripting

Target / Context

Comment Section of a blog, which is persistent and visible to every user of the app and is without proper output encoding and input validation

Mechanism

Application have some persistents fields in which if the user enter input it gets stored in the server or html code itself and is usually visible to multiple users on the application like the comments section, user bio, username section, etc. The attacker target such field if there is not proper output encoding and input validation present, they inject malicious scripts in such field which goes to the server which doesn't have proper encoding it processes it and stores it into the very html code like any other harmless input and as it is a script when a user load that page the script executes as the browser thinks that the maicious code is part of the site and this can lead to complete takeover of other user's account and information without the atttacker having to explicitly leading them to the compromised section 

Payload

<script>alert("Stored XSS by Prometheus")</script>

Root Cause

mainly Improper output encoding and a minor cause is lack of input validation

Why It Worked

in the comment section the attacker was able  input malcious script like in my POC  <script>alert("Stored XSS by Prometheus")</script> and when it reached the server the server without properly encoding the output just put it in the html code as the script was injected in a comment field which is persistent and accessible by every user and when a user accesses the page their browser thinks of it as part of the page and the parser executes it resulting in a XSS attack 

Detection Note (Defender's Lens)

logging should be done for every incoming and outgoing traffic, as all the malicious scipts are stored in the html the defender can grep for patterns like <script>, onerror=, javascript:, etc

Remediation

Setting up proper output encoding and input validation 