Just a markdown file that just contains all the bash stuff that I've done.

# Scripts:

#### Remove bad domains:

This script is to try to filter out all the domains I don't want to do anything further with since subfinder and crt.sh sometimes get domains such as cloudflare.

```bash
#!/usr/bin/env bash

# Meh, but should work for now

grep -Ev "innovationcast|blastheadrecords|cloudflare|quorum|pantheonsite|google|wix|wordpress|microsoft|incapsula|bluehost|certus|twitter|facebook|bit.ly|bitly|x.com|amazon|yahoo|youtube" "$1" | tee -a "$2"
```


### Update scripts:

#### Debian/Ubuntu:

```bash
#!/usr/bin/env bash

echo "[*] Starting system update"

sudo apt update && sudo apt --assume-yes upgrade
sudo apt --assume-yes dist-upgrade
sudo apt --assume-yes full-upgrade
sudo apt --assume-yes autoremove
sudo apt --assume-yes autoclean

echo "[*] Done"
```

**NOTE: Probably should write something for my EndeavourOS install which is what I run currently.**

#### Update git repos:

This is to try to update my 90 GB "Tools" folder where I keep tools that I've found and tested or kept for archiving (mostly through git):

```bash
#!/usr/bin/env bash

# Find all directories with .git and git pull any new changes

git config --global safe.directory '*'
find . -name .git -execdir git pull -v ';'
```

------

#### Bash aliases:

```bash
# Just some of my aliases I have in the bashrc file that I find useful

alias ls='ls --color=auto'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias grep_cidr="grep -a -o '[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\/[0-9]\{1,\}'"
alias grep_ip="grep -a -E -o '(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)'"
alias mkdir="mkdir -p"
alias shred="shred -uzf"
alias burp="/usr/local/bin/BurpSuiteCommunity"
alias john="/home/alex/Tools/john/run/john"
alias grep_email="grep -a -E -o '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b'"
```

**NOTE: I really need to update and clean up my .bashrc, but it is fine for now.**

------

#### Ohmybash:

Github: https://github.com/ohmybash/oh-my-bash
