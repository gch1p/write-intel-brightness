# write-intel-brightness

This is a script to control screen brightness on Lenovo ThinkPad X220 and similar after you changed PWM frequency by writing a custom value to 0xC8254 register. I use it with acpid.

The script reads current PWM frequency from the register, calculates correct new brightness level for `/sys/class/backlight/intel_backlight/brighness` and writes it.

### Usage

To increase brightness:
```
write-intel-brightness +
```

To decrease:
```
write-intel-brightness -
```

### acpid example

From `/etc/acpi/default.sh` on my Gentoo box:

```
case "$group" in
    video)
        case "$action" in
            brightnessup)
                /usr/local/bin/write-intel-brightness +
                ;;

            brightnessdown)
                /usr/local/bin/write-intel-brightness -
                ;;
        esac
        ;;
esac
```

### License

MIT
