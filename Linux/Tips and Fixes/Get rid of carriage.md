Apparently sometimes files/scripts have the \r at the end (I have no idea why. Think might be from copying and pasting from obsidian to my github account or something like that.)

Get rid with sed:

```bash
sed -i 's/\r$//' *.sh
```