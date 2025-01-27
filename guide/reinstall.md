<img align="right" src="https://github.com/n00b69/woa-lisa/blob/main/lisa.png" width="350" alt="Windows 11 running on a lisa">

# Running Windows on the Xiaomi 11 Lite NE 5G

## Reinstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modified recovery](https://github.com/n00b69/woa-lisa/releases/download/Files/modded-recovery-lisa.img)

### Boot into the modified recovery
> While in fastboot mode, replace `path\to\modded-recovery-lisa.img` with the actual path of the image
```cmd
fastboot boot path\to\modded-recovery-lisa.img
```

#### Formatting the Windows partition
```cmd
adb shell format
```

## [Next step: Reinstalling Windows](/guide/3-install.md)




















  
