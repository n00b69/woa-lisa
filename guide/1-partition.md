<img align="right" src="https://github.com/n00b69/woa-lisa/blob/main/lisa.png" width="350" alt="Windows 11 running on a lisa">

# Running Windows on the Xiaomi 11 Lite NE 5G

## Partitioning your device

### Prerequisites
- Unlocked bootloader

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modified recovery](https://github.com/n00b69/woa-lisa/releases/download/Files/modded-recovery-lisa.img) (You may need to flash official HyperOS if this image does not boot)

### Notes
> [!WARNING]  
> All your data will be erased! Back up now if needed.
> 
> Do not run the same command twice.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/lisawoa).
> 
> Do not run all commands at once, execute them in order!

> [!IMPORTANT]
> Make sure you use the MODDED Recovery throughout this whole tutorial as we provide tools to help aid this installation process and make it as easy as possible for you.
> 
> If you don't use it and you face any errors, consider it your fault and consider yourself alone if you try asking for support as you have deferred from the main guide.

### Opening CMD as an admin
> Download **platform-tools** and extract the folder somewhere, then open CMD as an **administrator**.
>
> It is recommended to keep this window open and use it throughout the entire guide.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
```

### Boot into the modified recovery
> While in fastboot mode, replace `path\to\modded-recovery-lisa.img` with the actual path of the image
```cmd
fastboot boot path\to\modded-recovery-lisa.img
```


> [!Important]
> If you get a black screen, try running the commands while on this black screen, as they may still work. If they don't, flash official HyperOS (2.0?) and try again.
>
> If the recovery still refuses to boot, follow [this guide](/guide/1-altpartition.md) instead.

#### Backing up your boot image
> This will back up your boot image in the current directory
```cmd
adb pull /dev/block/by-name/boot$(getprop ro.boot.slot_suffix) boot.img
```

### Partitioning your device
> There are two methods to partition your device. Please select the method you would like to use below. 

#### Method 1: Manual partitioning 

<details>
  <summary><strong>Click here for method 1</strong></summary> 

#### Resizing the partition table
```cmd
adb shell sgdisk --resize-table 64 /dev/block/sda
```

#### Opening a shell
```cmd
adb shell
```

### Preparing for partitioning
$${\color{lightblue}🟦 Note}$$
> If at any moment in parted you see an error prompting you to type "Yes/No" or "Ignore/Cancel", type `Yes` or `Ignore` depending on the situation to ignore the errors and continue.
>
> If you see any **udevadm** errors, you can ignore these as well.
```cmd
parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list
```cmd
print
``` 

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **33**
```cmd
rm $
``` 

#### Recreating userdata
> Replace **12.2GB** with the former start value of **userdata** which we just deleted
>
> Replace **70GB** with the end value you want **userdata** to have. In this example your available usable space in Android will be 70GB-12.2GB = **57.8GB**
```cmd
mkpart userdata ext4 12.2GB 70GB
``` 

#### Creating ESP partition
> Replace **70GB** with the end value of **userdata**
>
> Replace **70.3GB** with the value you used before, adding **0.3GB** to it
```cmd
mkpart esp fat32 70GB 70.3GB
``` 

#### Creating Windows partition
> Replace **70.3GB** with the end value of **esp**
```cmd
mkpart win ntfs 70.3GB -0MB
``` 

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be **34**
```cmd
set $ esp on
``` 

#### Exit parted
```cmd
quit
```

### Fixing the GPT
> If you do not do this, Windows may break your device
```cmd
adb shell fixgpt
```

### Formatting data
- Format all data in OrangeFox, or Android will not boot.
- ( Go to Wipe > Format data > type yes ) 

#### Check if Android still starts
- Just restart the phone, and see if Android still works 

### Formatting Windows and ESP drives
> Reboot into the modded recovery, then run the below two commands
```cmd
adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINLISA
``` 

```cmd
adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPLISA
``` 

</details>

#### Method 2: Automatic partitioning 

<details>
  <summary><strong>Click here for method 2</strong></summary> 

### Run the partitioning script
> Replace **$** with the amount of storage you want Windows to have (do not add GB, just write the number)
> 
> If it asks you to run it once again, do so
```cmd
adb shell partition $
``` 

### Check if Android still starts
- Just restart the phone, and see if Android still works 

</details>

## [Next step: Rooting your phone](2-root.md)



















