# surface-pro-11-dual-boot-instructions
These are instructions for configuring a Surface Pro 11 to dual boot Windows 11

## What you will need prior to starting
- Windows 11 ARM-64 ISO

- Your bitlocker recovery keys

- A USB Thumbdrive minimum 32GB
    
- Surface Pro 11 Drivers from [here](https://www.microsoft.com/en-us/download/details.aspx?id=106119&msockid=3df1bb07c1386c68124baeefc0186dad)


## Create the recovery drive

1. In the search box on the taskbar, enter **recovery drive**, then select Create a recovery drive or Recovery Drive from the results. You might be asked to enter an admin password or confirm your choice.

2. In the User Account Control box, select Yes.

3. Make sure to clear the Back up system files to the recovery drive check box and then select Next.

![](/images/image1.png)

4. Select your USB drive, and then select Next.

![](/images/image2.png)

5. Click Create

![](/images/image3.png)

***Some utilities need to be copied to the recovery drive, so this might take a few minutes.***

6. When the recovery drive is ready, select Finish.

![](/images/image4.png)


## Mount the Windows 11 ARM-64 ISO

1. Double click on your Windows 11 ARM-64 ISO. Windows 11 will mount it.

2. In the User Account Control box, select Yes.

3. Copy all of the files from the mounted ISO.

![](/images/image5.png)

4. Open your recovery drive and paste all the files from the ISO.

![](/images/image6.png)

5. Select **Skip** when notified that instll.wim is too large.

![](/images/image7.png)

6. When prompted to overwrite the files, choose **Replace the files in the destination**

![](/images/image8.png)


## Convert install.wim to a split .swm file

1. Open an elevated command prompt.

2. Use DISM to split the install.wim file from your ISO and save it as mutiple smaller .swm files on your recvery drive.

```
Dism /Split-Image /ImageFile:D:\sources\install.wim /SWMFile:E:\sources\install.swm /FileSize:4000 
```

NOTE: Replace the drive letters in the code above to match the drive letters assigned to your Recovery and ISO drives.

![](/images/image9.png)

3. Be sure to copy your Surface drivers to your recovery drive as the ISO install will not have these and you will not have wireless drivers to download them on the new OS.

![](/images/image10.png)

## Shrink your C: drive

1. Right click on start and select disk management

![](/images/image12.png)

2. Right click on your C: Drive and select Shrink volume.

![](/images/image11.png)

3. Select the desired amount of space to shrink.
***My drive was 1TB so I split it 499000***

NOTE: Do not format the drive. You will select it when you are in the Windows 11 installer on the next section.


## Boot in to recovery

1. Go to Settings, click on System and then Recovery.

![](/images/image13.png)

2. Select Restart now under Advanced Startup

![](/images/image14.png)

***This will boot your Surface to the recovery drive and begin the Windows 11 install.***

**When prompted to select the install location, chood the blank partition you created when you shrank the C: drive.**

## Label your Operating Systems

After you have installed Windows and added your drivers, you will have to Operating Systems both call Windows 11. To make it easier to identify them you can give the names.

1. Open and elevated command prompt.

2. Use BCDEDIT to view the operating systems.

```
bcdedit /Enum /v
```

3. Make note of the Operating System Identifiers as you will need them in the next step.

![](/images/image15.png)

4. Use BCDEDIT to assign names to each OS.

```dotnetcli
bcdedit /set {b0b3339b-2dc9-11f0-bcf2-ca9af914c2b7} description "Work"

bcdedit /set {7f62d4dc-2dd7-11f0-9b7c-ad12802c178b} description "Home"
```













