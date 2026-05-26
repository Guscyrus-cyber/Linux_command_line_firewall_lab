**Linux Command-Line Firewall & Network Investigation Lab**

In this realistic Linux terminal command line operations lab, we simulate how a SOC analyst or network security analyst investigates firewall and network traffic directly from the Linux command line without using a SIEM platform. The lab focuses on real-world firewall logs containing allowed and blocked network connections, suspicious source IP addresses, destination ports, protocols, applications, and user activity. Instead of graphical dashboards, all investigations are performed using terminal tools such as grep, awk, cat, sort, uniq, wc, head, and tail.

The purpose of this lab is to teach how security analysts investigate suspicious traffic, identify blocked attacks, analyze targeted ports, review user connections, and trace network activity through raw firewall logs. The dataset contains realistic examples of SSH attacks, RDP connection attempts, SMB targeting, FTP scans, Telnet access attempts, HTTPS traffic, DNS requests, cloud connections, and other network events commonly seen inside enterprise environments.

Throughout the lab, analysts perform investigations such as identifying attacker IP addresses, counting blocked connections, analyzing protocols, reviewing encrypted traffic, examining targeted services, and building simple attack timelines directly from the terminal. This helps develop important Linux command-line investigation skills used in SOC operations, incident response, firewall monitoring, threat hunting, and blue-team analysis.

This lab also introduces the concept of working with structured log data in a realistic operational environment. Each log entry contains fields such as source IP, destination IP, protocol, destination port, application name, action type, and transferred bytes, allowing analysts to practice filtering, parsing, counting, and extracting important security information from raw data.

By the end of this terminal-based investigation lab, the analyst gains hands-on experience performing firewall and network investigations using native Linux tools, understanding suspicious traffic patterns, recognizing common attack targets, and building foundational operational skills commonly used in Linux-based SOC and incident response environments.\
\
Creating this new realistic firewall/network investigation dataset first:\
\
cd ~/Downloads\
mkdir firewall_investigation_lab\
cd firewall_investigation_lab\
nano firewall_logs.log\
\
2026-05-21T08:00:01 action=ALLOW src_ip=192.168.1.10 dst_ip=8.8.8.8 protocol=UDP src_port=51514 dst_port=53 bytes=120 user=john app=DNS

2026-05-21T08:01:15 action=BLOCK src_ip=45.33.22.11 dst_ip=192.168.1.20 protocol=TCP src_port=4444 dst_port=22 bytes=0 user=unknown app=SSH

2026-05-21T08:02:22 action=ALLOW src_ip=192.168.1.15 dst_ip=142.250.190.78 protocol=TCP src_port=51515 dst_port=443 bytes=2048 user=alice app=HTTPS

2026-05-21T08:03:41 action=BLOCK src_ip=185.220.101.45 dst_ip=192.168.1.25 protocol=TCP src_port=5555 dst_port=3389 bytes=0 user=unknown app=RDP

2026-05-21T08:04:18 action=ALLOW src_ip=192.168.1.25 dst_ip=17.253.144.10 protocol=TCP src_port=51516 dst_port=443 bytes=4096 user=bob app=HTTPS

2026-05-21T08:05:55 action=BLOCK src_ip=77.77.77.77 dst_ip=192.168.1.30 protocol=TCP src_port=6666 dst_port=21 bytes=0 user=unknown app=FTP

2026-05-21T08:06:10 action=ALLOW src_ip=192.168.1.40 dst_ip=151.101.1.69 protocol=TCP src_port=51517 dst_port=80 bytes=1024 user=carol app=HTTP

2026-05-21T08:07:33 action=BLOCK src_ip=123.123.123.123 dst_ip=192.168.1.50 protocol=TCP src_port=7777 dst_port=445 bytes=0 user=unknown app=SMB

2026-05-21T08:08:11 action=ALLOW src_ip=192.168.1.55 dst_ip=52.95.110.1 protocol=TCP src_port=51518 dst_port=443 bytes=8192 user=david app=AWS

2026-05-21T08:09:44 action=BLOCK src_ip=91.214.124.10 dst_ip=192.168.1.60 protocol=TCP src_port=8888 dst_port=3306 bytes=0 user=unknown app=MYSQL

2026-05-21T08:10:21 action=ALLOW src_ip=192.168.1.70 dst_ip=104.244.42.1 protocol=TCP src_port=51519 dst_port=443 bytes=3500 user=emma app=SOCIAL

2026-05-21T08:11:57 action=BLOCK src_ip=66.66.66.66 dst_ip=192.168.1.80 protocol=TCP src_port=9999 dst_port=23 bytes=0 user=unknown app=TELNET

2026-05-21T08:12:35 action=ALLOW src_ip=192.168.1.90 dst_ip=13.107.42.14 protocol=TCP src_port=51520 dst_port=443 bytes=5000 user=frank app=OFFICE365

2026-05-21T08:13:42 action=BLOCK src_ip=201.201.201.201 dst_ip=192.168.1.95 protocol=TCP src_port=1010 dst_port=5900 bytes=0 user=unknown app=VNC

2026-05-21T08:14:55 action=ALLOW src_ip=192.168.1.100 dst_ip=172.217.14.206 protocol=TCP src_port=51521 dst_port=443 bytes=9000 user=grace app=GOOGLE\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
\
\
The dataset structure;

| **Field** | **Value** |
|-----------|-----------|
| \$1       | timestamp |
| \$2       | action    |
| \$3       | src_ip    |
| \$4       | dst_ip    |
| \$5       | protocol  |
| \$6       | src_port  |
| \$7       | dst_port  |
| \$8       | bytes     |
| \$9       | user      |
| \$10      | App       |

Using this command:\
awk '{print \$X}' firewall_logs.log \| sort \| uniq\
This command extracts and displays unique values from a specific field in the firewall logs, where X represents the field (column) number to investigate.\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
This dataset is good for:

grep\
awk\
sed\
cut\
sort\
uniq\
wc\
head\
tail\
tr\
column\
investigation filtering\
blocked traffic analysis\
suspicious IP hunting\
protocol investigation\
port investigation\
user activity review\
threat hunting\
firewall log parsing\
SOC-style CLI investigations\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**\
\**
Last login: Thu May 21 21:15:02 on ttys000

Guscyrus@SOC-Lab:~ \$ cd ~/Downloads

Guscyrus@SOC-Lab:~/Downloads \$ mkdir firewall_investigation_lab

Guscyrus@SOC-Lab:~/Downloads \$ cd firewall_investigation_lab

Guscyrus@SOC-Lab:~/Downloads/firewall_investigation_lab \$ nano firewall_logs.log

Guscyrus@SOC-Lab:~/Downloads/firewall_investigation_lab \$ ls -lh

total 8\
-rw-r--r-- 1 Guscyrus staff 2.1K May 21 21:28 firewall_logs.log**\**
\
**\**
<img src="Linux_firewall_images/media/image1.png" style="width:6.5in;height:2.89375in" alt="A screenshot of a computer Description automatically generated" />**\
\**
Last login: Thu May 21 21:59:01 on ttys000

Guscyrus@SOC-Lab:~ \$ cd ~/Downloads/firewall_investigation_lab

Guscyrus@SOC-Lab:~/Downloads/firewall_investigation_lab \$ ls -lh

total 8

-rw-r--r-- 1 Guscyrus staff 2.1K May 21 21:28 firewall_logs.log\
\
<img src="Linux_firewall_images/media/image2.png" style="width:6.5in;height:2.61875in" alt="A screenshot of a computer Description automatically generated" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
View the Dataset\
\
Bash:\
cat firewall_logs.log

Displays all firewall logs\
Analyst reviews all traffic events\
\
\
<img src="Linux_firewall_images/media/image3.png" style="width:6.5in;height:1.81181in" alt="A screenshot of a computer Description automatically generated" />\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
**Top of FormCount Total Events**\
\
Bash:

wc -l firewall_logs.log

Counts total log entries\
Helps analyst know log volume\
15 firewall events recorded\
\
<img src="Linux_firewall_images/media/image4.png" style="width:6.5in;height:0.45486in" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**Find Blocked Traffic\
\**
Bash:

grep "action=BLOCK" firewall_logs.log

Shows blocked/suspicious traffic\
Firewall denied these connections

RDP\
SSH\
FTP\
SMB\
MYSQL\
TELNET\
VNC

External systems attempted dangerous access\
\
\
<img src="Linux_firewall_images/media/image5.png" style="width:6.5in;height:0.91806in" alt="A screenshot of a computer Description automatically generated" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Count Blocked Attempts\
\
Bash:

grep "action=BLOCK" firewall_logs.log \| wc -l

Counts total blocked attacks

Firewall blocked 7 suspicious connections\
\
\
<img src="Linux_firewall_images/media/image6.png" style="width:6.5in;height:0.91806in" alt="A screenshot of a computer Description automatically generated" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Find Suspicious Source Ips\
\
Bash:

grep "action=BLOCK" firewall_logs.log \| awk '{print \$3}'

Extracts attacker source IPs

These source ip attempted attacks\
src_ip=45.33.22.11\
src_ip=185.220.101.45\
src_ip=77.77.77.77\
src_ip=123.123.123.123\
src_ip=91.214.124.10\
src_ip=66.66.66.66\
src_ip=201.201.201.201\
\
{print \$3} in the awk command means “print the third field (third column) from each matching log line,” and because the firewall logs contain 7 blocked attack lines, the third field displayed 7 different attacker source IP addresses.\
\
<img src="Linux_firewall_images/media/image7.png" style="width:6.5in;height:0.75in" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Finding Most Targeted Ports

Bash:

grep "action=BLOCK" firewall_logs.log \| grep -o 'dst_port=\[0-9\]\*'

Shows targeted destination ports\
\
dst_port=22\
dst_port=3389\
dst_port=21\
dst_port=445\
dst_port=3306\
dst_port=23\
dst_port=5900

Attackers targeted these ports

| 22  | SSH | Secure remote Linux login |
|-----|-----|---------------------------|

| 3389 | RDP | Remote Desktop Protocol (Windows remote access) |
|------|-----|-------------------------------------------------|

| 21  | FTP | File Transfer Protocol |
|-----|-----|------------------------|

| 445 | SMB | Windows file sharing |
|-----|-----|----------------------|

| 3306 | MySQL | Database service |
|------|-------|------------------|

| 23  | Telnet | Unencrypted remote login |
|-----|--------|--------------------------|

| 5900 | VNC | Remote desktop/control service |
|------|-----|--------------------------------|

<img src="Linux_firewall_images/media/image8.png" style="width:6.5in;height:0.77222in" />**\**
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\
\**
Investigate SSH Attacks

Bash:

grep "dst_port=22" firewall_logs.log

Investigates SSH attack attempts\
Hacker attempted remote SSH access\
\
<img src="Linux_firewall_images/media/image9.png" style="width:6.5in;height:0.54167in" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
Investigate RDP Attacks

Bash:

grep "dst_port=3389" firewall_logs.log

Looks for Remote Desktop attacks\
That’s a Common attacker technique\
\
\
<img src="Linux_firewall_images/media/image10.png" style="width:6.5in;height:1.44167in" alt="A screenshot of a computer Description automatically generated" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
Showing Allowed Traffic Only

Bash:

grep "action=ALLOW" firewall_logs.log

Displaying legitimate traffic\
Normal employee/business connections\
\
\
<img src="Linux_firewall_images/media/image11.png" style="width:6.5in;height:0.95625in" alt="A close up of a text Description automatically generated" />\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
Finding HTTPS Traffic

Bash:

grep "dst_port=443" firewall_logs.log

Investigates encrypted HTTPS traffic\
It Users accessed secure websites/cloud services\
\
<img src="Linux_firewall_images/media/image12.png" style="width:6.5in;height:0.95625in" alt="A close up of a text Description automatically generated" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Listing Unique users

Bash:

awk '{print \$9}' firewall_logs.log \| sort \| uniq

Listing unique users\
It Shows users\
\
user=alice\
user=bob\
user=carol\
user=David\
user=emma\
user=frank\
user=grace\
user=john\
user=unknown\
\
<img src="Linux_firewall_images/media/image13.png" style="width:6.5in;height:1.95556in" alt="A screenshot of a computer Description automatically generated" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Listing Unique Applications\
\
awk '{print \$10}' firewall_logs.log \| sort \| uniq\
\
app=AWS

app=DNS

app=FTP

app=GOOGLE

app=HTTP

app=HTTPS

app=MYSQL

app=OFFICE365

app=RDP

app=SMB

app=SOCIAL

app=SSH

app=TELNET

app=VNC\
\
<img src="Linux_firewall_images/media/image14.png" style="width:6.5in;height:1.5875in" alt="A screenshot of a computer Description automatically generated" />\
\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
Listing Uniques source IP Addresses\
\
Command:\
\
awk '{print \$3}' firewall_logs.log \| sort \| uniq\
\
in this firewall investigation dataset, \$3 contains the src_ip field, and for the blocked traffic logs those source IPs represent the attacker or suspicious external IP addresses attempting unauthorized connections.\
\
src_ip=123.123.123.123

src_ip=185.220.101.45

src_ip=192.168.1.10

src_ip=192.168.1.100

src_ip=192.168.1.15

src_ip=192.168.1.25

src_ip=192.168.1.40

src_ip=192.168.1.55

src_ip=192.168.1.70

src_ip=192.168.1.90

src_ip=201.201.201.201

src_ip=45.33.22.11

src_ip=66.66.66.66

src_ip=77.77.77.77

src_ip=91.214.124.10\
\
<img src="Linux_firewall_images/media/image15.png" style="width:6.5in;height:1.56667in" alt="A screenshot of a computer Description automatically generated" />\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
Finding Largest Data Transfers

Command:

sort -t= -k9 -n firewall_logs.log

Helps identify large traffic transfers\
Useful in exfiltration investigations\
\
\
<img src="Linux_firewall_images/media/image16.png" style="width:6.5in;height:1.51319in" alt="A screenshot of a computer Description automatically generated" />\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

Real SOC Investigation Example

Command:

grep "dst_port=445" firewall_logs.log

Investigates possible lateral movement or ransomware activity

| src_ip=123.123.123.123 | Attacker/source system                |
|------------------------|---------------------------------------|
| dst_ip=192.168.1.50    | Target/victim internal machine        |
| protocol=TCP           | Communication used TCP protocol       |
| src_port=7777          | Random source port opened by attacker |
| dst_port=445           | SMB service targeted                  |
| action=BLOCK           | Firewall blocked the attack           |

dst_ip=192.168.1.50 = the internal device being targeted\
protocol=TCP = the network protocol used\
src_port=7777 = temporary/random port used by attacker to initiate the connection\
src_ip = who initiated the connection\
dst_ip = who received/was targeted by the connection\
src_port = attacker/client-side temporary port\
dst_port = service being targeted on victim machine\
\
The command:

grep "dst_port=445" firewall_logs.log

searched the firewall logs for traffic targeting destination port 445, which is the SMB (Server Message Block) service used for Windows file sharing.

The output shows that the source IP address:

123.123.123.123

attempted the SMB attack because it tried to connect to destination port 445, and the firewall blocked the connection.\
\
<img src="Linux_firewall_images/media/image17.png" style="width:6.5in;height:0.33264in" />\
\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\
\
\
Timeline Investigation\
\
Command:

head firewall_logs.log

or

tail firewall_logs.log

Reviews first or latest events\
Helps analyst build timeline

<img src="Linux_firewall_images/media/image18.png" style="width:6.5in;height:2.03542in" alt="A screenshot of a computer code Description automatically generated" />

Top of Form

Bottom of Form

What was this lab about:

Firewall analysis\
Threat hunting\
SOC investigations\
Network investigation\
Port analysis\
IP investigation\
Log parsing\
Linux CLI skills\
Blue-team investigations\
Incident response basics

**Main Terminal Tools Used**

| **Tool** | **Purpose**       |
|----------|-------------------|
| cat      | View logs         |
| grep     | Search logs       |
| awk      | Extract fields    |
| wc       | Count events      |
| sort     | Organize data     |
| uniq     | Remove duplicates |
| head     | First events      |
| tail     | Latest events     |
