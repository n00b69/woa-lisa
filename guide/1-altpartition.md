<img align="right" src="https://github.com/n00b69/woa-lisa/blob/main/lisa.png" width="350" alt="Windows 11 running on a lisa">

# Running Windows on the Xiaomi 11 Lite NE 5G

## Partitioning your device (alternative method, if recovery does not boot)

### Prerequisites
- Unlocked bootloader & root access

- [Termux](https://play.google.com/store/apps/details?id=com.termux)

- [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK)

### Notes
> [!WARNING]
> All your data will be erased! Back up now if needed.
> 
> Do not run the same command twice.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/lisawoa).
> 
> Do not run all commands at once, execute them in order!

### Backing up important partitions
- Download and install the **WOA Helper** app, then open it and grant it root access.
- Click on **BACK UP BOOT.IMG** and select **ANDROID**.
- Navigate to the `WOAHelper/backups` folder in your internal storage and copy its contents to your PC.

### Setting up Termux
- Download Termux if you haven't already.
- In Termux, run the following commands:
> If there are any Y/N prompts, type Y
```cmd
pkg install root-repo
```
```cmd
pkg install parted
```
```cmd
pkg install gptfdisk
```
```cmd
pkg install ntfs-3g
```
```cmd
pkg install dosfstools
```
> After running the below command, accept the root access popup if you haven't already done so earlier.
```cmd
su
```

#### Resizing the partition table
```cmd
sgdisk --resize-table 64 /dev/block/sda
```

### Preparing for partitioning
> [!Note]
>
> If at any moment in parted you see an error prompting you to type "Yes/No" or "Ignore/Cancel", type `Yes` or `Ignore` depending on the situation to ignore the errors and continue.
>
> If you see any **udevadm** errors, you can ignore these as well.
```cmd
/data/data/com.termux/files/usr/bin/parted /dev/block/sda
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
- Run the below command to open gdisk in **sda** (later this command will be reused to open *sdb**, **sdc** etc.).
```cmd
gdisk /dev/block/sda
```
- Run the below commands (each letter is an individual command).
```cmd
x
```
```cmd
j
```
```cmd
enter (do not actually write enter)
```
```cmd
k
```
```cmd
enter (do not actually write enter)
```
```cmd
w
```
```cmd
y
```
- Repeat this process for sdb, sdc, sdd, sde, sdf, sdg etc. until it throws an error that the disk does not exist.

### Formatting Windows and ESP drives
```cmd
mkfs.ntfs -f /dev/block/sda35 -L WINLISA
``` 
```cmd
mkfs.fat -F32 -s1 /dev/block/sda34 -n ESPLISA
``` 

#### Check if Android still starts
- Just restart the phone, and see if Android still works.
- If it doesn't, boot into (stock) recovery to perform a factory reset.

## [Next step: Installing Windows](3-install.md)















