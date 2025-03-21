<img align="right" src="https://github.com/n00b69/woa-lisa/blob/main/lisa.png" width="350" alt="Windows 11 running on a lisa">

# Running Windows on the Xiaomi 11 Lite NE 5G

## Uninstallation

### Why is this needed?
If you want to uninstall Windows, this is used instead of deleting partitions manually to avoid human error + writing a whole dedicated guide to just uninstalling.

If you want to relock your bootloader you'll need your partition table to be stock.

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modified recovery](https://github.com/n00b69/woa-lisa/releases/download/Files/modded-recovery-lisa.img) (new method)

- [gpt_both0.bin](https://github.com/n00b69/woa-vayu/releases/download/Files/gpt_both0.bin) (old method)

## New method

### Switch to Android
> Or your device will not boot into Android after uninstalling Windows
- Run the **Switch to Android** or **Android** shortcut on your desktop, or flash a **boot.img** backup in fastboot/recovery.

### Boot into the modified recovery
> While in fastboot mode, replace `path\to\modded-recovery-lisa.img` with the actual path of the image
```cmd
fastboot boot path\to\modded-recovery-lisa.img
```

### Execute the restore script
```cmd
adb shell restore
```

##### Finished!

## Old method 
> In case the new one didn't work

### Switch to Android
> Or your device will not boot into Android after uninstalling Windows
- Run the **Switch to Android** or **Android** shortcut on your desktop, or flash a **boot.img** backup in fastboot/recovery.

### Boot into fastboot mode
> Hold the **volume down** + **power button** while the phone is turned off, or run the following command while it is booted
```cmd
adb reboot bootloader
```

### Restore GPT
> Replace `path\to\gpt_both0.bin` with the path of the **gpt_both0.bin** file
```cmd
fastboot flash partition:0 path\to\gpt_both0.bin
```

#### Erase userdata
> To avoid a bootloop and restore FS size
```cmd
fastboot -w
```

##### Finished!









