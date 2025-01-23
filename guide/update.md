<img align="right" src="https://github.com/n00b69/woa-lisa/blob/main/lisa.png" width="350" alt="Windows 11 running on a lisa">

# Running Windows on the Xiaomi 11 Lite NE 5G

## Updating drivers

### Prerequisites
- [Modified recovery](https://github.com/n00b69/woa-lisa/releases/download/Files/modded-ofox-lisa.zip)

- [Drivers](https://github.com/n00b69/woa-vayu/releases/tag/Drivers)

- [UEFI image](https://github.com/n00b69/woa-vayu/releases/tag/UEFI)

### Boot into the modified recovery
> While booted in Android
```cmd
adb reboot recovery
```

#### Execute the msc script
> If it asks you to run it once again, do so
```cmd
adb shell msc
```

### Diskpart
```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace "$" with the actual number of **WINLISA**
```diskpart
select volume $
```

#### Assign the letter X
```diskpart
assign letter x
```

#### Exit diskpart
```diskpart
exit
```

### Installing drivers
> [!Note]
> This process will take +- 30 minutes. Do not worry, this is normal.

- Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINLISA** (which should be **X**), then press enter

### Reboot your device
> Make sure to also change the UEFI image in Android, otherwise you may face a "blue screen of death" (BSoD) when booting Windows later.
```cmd
adb reboot
```

## Finished!













