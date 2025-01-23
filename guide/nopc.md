<img align="right" src="https://github.com/n00b69/woa-lisa/blob/main/lisa.png" width="350" alt="Windows 11 running on a lisa">

# Running Windows on the Xiaomi 11 Lite NE 5G

## Installing Windows without a PC

### Prerequisites
- Unlocked bootloader & rooted phone

- [Modified recovery](https://github.com/n00b69/woa-lisa/releases/download/Files/modded-ofox-lisa.zip)

- [Lisa WinInstaller](https://github.com/n00b69/releases/download/Files/LisaWinInstaller.zip)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)

- [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK)

### Notes
> [!WARNING]  
> All your data will be erased! Back up now if needed.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woalisa).

### Flash and boot into the modified recovery
> If you aren't rooted yet, do this first
- Open **Magisk** and select the **Modules** tab.
- Click on **Install from storage** and locate `modded-ofox-lisa.zip` and install it.
- Return to the main menu, press the rotating arrow icon in the top right, and press `Reboot Recovery`.

#### Opening OrangeFox terminal
- Once booted into OrangeFox, decrypt data by entering your password if it asks you to.
- Press the **Advanced** button on the bottom right of the screen, then press **Terminal**

### Run the partitioning script
> Replace **$** with the amount of storage you want Windows to have (do not add GB, just write the number)
> 
> If it asks you to run it once again, do so
```cmd
partition $
```

### Check if Android still starts
- Just restart the phone, and see if Android still works

### Preparing necessary files
- Download the Windows image and make sure it remains in the `Download` folder **of your internal storage**, NOT SD card.
- Download **WinInstaller** and leave it in your internal storage.
- Download and install the [WOA Helper app](https://github.com/n00b69/woa-helper/releases/tag/APK), then open it and grant it root access. Do not do anything else inside the app yet.
- Reboot to the modified OrangeFox. Flash it again if it has been replaced by MIUI recovery.

### Flashing WinInstaller
- In OrangeFox, select **Install** and then locate **WinInstaller.zip**.
- Wait until all processes complete and your device boots into Windows. This will take around 15-20 minutes.

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.
>
> If there is no such button, press the **SIM card** button at the top of the screen (the one that says **Connected**), and press **Disconnect**.

#### Booting to Android
- Run the **Android** shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access).

#### Booting to Windows
- Press **QUICKBOOT TO WINDOWS** inside the WOA Helper app, or use the newly created toggle in your quick settings panel.

## Finished!


























