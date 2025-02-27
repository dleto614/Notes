#### Install OS:

To start the installation:

```bash
mkdir debian-bookworm-mipsel
qemu-img create -f qcow hda.img 10G
qemu-system-mipsel -M malta -hda hda.img -net nic -kernel vmlinuz-6.1.0-29-4kc-malta   -initrd initrd.gz   -append "root=/dev/sda console=ttyS0" -nographic
```

**NOTE: In order for serial to work user must be in the group. For Arch Linux this is 'uucp' and for Debian this is 'dialout'**

To add:

```bash
sudo usermod -aG uucp $USER
sudo usermod -aG dialout $USER
```

------

#### Extract required files:

To mount the qcow hard drive:

```bash
sudo pacman -Sy nbd && sudo reboot now
sudo modprobe nbd max_part=16
sudo qemu-nbd -c /dev/nbd0 hda.img
sudo  partprobe /dev/nbd0
sudo fdisk -l /dev/nbd0
sudo  mount /dev/nbd0p1 /mnt/firmware/
```

To copy over the kernal and initrd from qcow hard drive:

```bash
ls /mnt/firmware/
cd /to/directory/of/qemu/os
mkdir output

# Copy over the kernel and initrd
cp /mnt/firmware/boot/vmlinuz-6.1.0-* output/
cp /mnt/firmware/boot/initrd.img-6.1.0-* output/
```

------

#### Boot into Debian:

To boot into the Debian MIPS build:

```bash
qemu-system-mipsel -M malta   -hda hda.img   -net nic   -net user,hostfwd=tcp::2222-:22 -kernel output/vmlinuz-6.1.0-29-4kc-malta -initrd output/initrd.img-6.1.0-29-4kc-malta  -append "root=/dev/sda1" -m 512 -nographic
```

------

#### Firmware:

Upload to debian:

```bash
scp -P 2222 squashfs-root.tar alex@localhost:/tmp/squashfs-root.tar

# On debian extract the tar
tar xvf /tmp/squashfs-root.tar
```

#### Mount and chroot:

```bash
sudo mount -o bind /dev ./squashfs-root/dev
sudo mount -t proc /proc ./squashfs-root/proc
sudo mount -o bind /sys ./squashfs-root/sys
sudo chroot ./squashfs-root/ /bin/sh
```

**NOTE: Might have to adjust this to get a shell**