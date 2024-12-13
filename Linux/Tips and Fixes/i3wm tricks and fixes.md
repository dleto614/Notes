## Brightness:

Install <mark style="background: #FF5582A6;">brightnessctl</mark> and set the key binds to the brightness up and down buttons if they are on the keyboard.

```bash
bindsym XF86MonBrightnessUp exec --no-startup-id brightnessctl set +5%
bindsym XF86MonBrightnessDown exec --no-startup-id brightnessctl set 5%-
```

------