---
Name: Syncting
Platform: Linux
tags:
  - Resources
---
Syncthing is an open source tool that lets you sync files and directories between computers.

Usually I run it locally and sync between my computers mostly for my Obsidian notes, Tools folder, and Music folder.

To install on Arch Linux:

```bash
sudo pacman -Sy syncthing
```

------

On Debian:

```bash
curl -s https://syncthing.net/release-key.txt | sudo apt-key add -
echo "deb https://apt.syncthing.net/ syncthing stable" | sudo tee /etc/apt/sources.list.d/syncthing.list
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install syncthing
```

------

To enable and start as a service:

```bash
sudo systemctl enable syncthing@${USER}.service
sudo systemctl start syncthing@${USER}.service
```

------

To get access to the web ui navigate to `127.0.0.1:8384` in the browser.

**NOTE: It is recommended to setup a username and password for the web ui. Which can be done in the settings**

------

Pretty straightforward to add device and start syncing after approving of devices to join.

Website: https://syncthing.net/
Docs here: https://docs.syncthing.net/