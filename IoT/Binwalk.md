#### Install:

(This is for Arch Linux and it would be different on Debian)

```bash
sudo pacman -Sy sasquatch-git binwalk
yay -Sy jefferson
```

- Install sasquatch to extract squashfs
- Install jefferson to extract `jffs2`

There is probably a better way like the docker image, but this is how I am doing it for now on my Thinkpad.

#### Extract

```bash
binwalk -Me firmware.bin
```

Can be a different file with different extension, but works for the most part. There are probably some packages I am missing that are for different filesystems, but haven't had a chance yet to work with them so haven't run into the errors yet in binwalk.