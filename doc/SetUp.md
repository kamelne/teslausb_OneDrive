# Set Up Raspberry PI
There are Three phases to setting up the Pi:
1. Get the OS onto the micro sd card.
2. Get a shell on the Pi.
3. Set up the archive for dashcam clips.
4. Set up the USB storage functionality.

### Get OS on SD Card
1. Download the [latest teslausb image](https://github.com/marcone/teslausb/releases) and a flashing/imaging tool. I used [Raspberry Pi Imager](https://github.com/marcone/teslausb/releases)

2. Attached SD card to computer and use imager to erase and format the card. Select Raspberry Pi Zero 2 W and scroll down under Operating System to find erase. Be sure to select the correct storage device as this will erase all information on the drive. 

![rpiErase](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/8bbe9d88-2d48-4444-9df1-42df59b5b689)

3. After formatting the drive Under Operating System scroll down to Use custom and locate where you save the teslausb image. Select the Storage drive you formatted in the previous step.

![rpiImage](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/e9fdab14-c572-4480-a5bf-b914926ebf25)

4. Once the SD card has been imaged and verified, disconnect then reconnect it and you will see a new drive called "bootfs". Here you will replace the teslausb_setup_variables.conf file with the one I have attached and made a few edits using notepad or a text editor of your choice.

[sample setup variables](doc/teslausb_setup_variables.conf)

- The changes I made are to comment out the use of CIFS and uncomment rclone archiving, we will update the other variables later in the set up. 

![addrclone](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/cb4c6846-9bed-4f45-80da-c4338b0e27c4)

  
- Choose Partition Sizing, I choose most of the Camera storage and some for BoomBox files. You can change these numbers if you plan on having music on your drive. *I have not tested the Music folder syncing with OneDrve

![partitionsizing](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/2222a720-c662-4805-89d1-5679e1a5e06c)


- Set Wifi SSID and Password, replace everything within the quotes with you SSID and Password

![ssid](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/6753560b-2b1d-4d0b-ae64-908ab858bf91)

- Use ExFat filesystem, might not be necessary but my SD card was also in ExFat format

![exfat](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/f580a8b8-e777-466f-8df5-6b05f4e0f865)


5. After the changes were saved to the files and replace on the SD card you can eject it and insert it into the Raspberry Pi, power on the pi and wait for the teslausb to be installed. Could take over five minutes, to know when the drive is connected you can check if it is recognized on you router or if you are able to successfully able to ssh in the next step.

### Get a shell on the Pi.
These steps are you windows, for mac you can see [barjohn's guide](https://github.com/barjohn/MarconeTeslausb/blob/master/doc/GetShellWithoutMonitorOnWindows.md)

1. Launch PowerShell as administrator, right click on title bar and check under properties that 'Use Legacy console" is unchecked.
2. Run this command and press Y when prompted

  `Set-ExecutionPolicy -Scope CurrentUser Unrestricted`

3. In PowerShell ssh to connect to the raspberry pi:
   
  `ssh pi@teslausb.local` 

  if you get a 'host id' error delete the "users\USERNAME\.ssh\known_hosts" file

  default password is:   `raspberry`

* It is recommended to change the password but not necessary, this can be done by enter `passwd` and following the steps

  4. Become root user by running
  
  `sudo -i`
  
  *you will remain in the root user account for the rest of the steps

  ### Set up the archive for dashcam clips.

1. While still in root user run the following command:

`curl -L https://raw.github.com/pageauc/rclone4pi/master/rclone-install.sh | bash`

2. The next step gave me a bit of trouble as the rclone config did not launch a browser for me to be able to authenticate my OneDrive account. I will give both methods:

   a. run the below and follow the steps:

   `rclone config`

     1. Create new remote option 'n'
     2. Name the remote 'ANY_NAME'
     3. For type of storage use '34'
     4. Leave  client_id and client_secret blank, just hit enter
     5. For region select which is best for you, I am in the US and I used '1'
     6. Advanced Config 'n'
     7. web browser 'y' here is where the browser would not launch for me and the provided link did not connect either, if it works for you log into your OneDrive. If unable to launch browser press 'ctrl + C' to stop the config process and skip to b.
     8. Select the correct connect for me '1'
     9. Select the drive you created earlier '1'
     10. Then 'Y' for the next two prompts
  
    b. What worked me was creating the rclone.conf file on windows and manually adding it and the directory to the Pi:
   
     1. Download (rclone for windows](Run rclone.exe config)
     2. Extract the rclone.exe file to somewhere you can find
     3. Open Command Prompt as administrator and go to the directory you extracted rclone.exe and run

        `start rclone.exe config`

     4. Here a browser will launch for you to log into OneDrive the follow the steps above to complete the setup
     5. locate the conf file created and open with a text editor, default location is

        `Users\NAME\AppData\Roaming\rclone`
        
     7. Back on the PowerShell, from the root user check that you are in the root directory with "pwd" then run the following

         ```
         mkdir /.config
         cd /.config
         mkdir rclone
         cd rclone
        ```
         
     8. Now open nano to create rclone.conif file in Pi
        ``` nano ```

        open the rclone.conf file on your pc and copy all the contents

        on PowerShell right click the title bar, then edit paste. You should see all the content in the PowerShell nano file

     9. Press 'ctrl + O" to name the file 'rclone.conf' then 'control + X' to exit
     10. Finally run these commands, you can change the name and path if you would like:

        
        export RCLONE_DRIVE=onedrive
        export RCLONE_PATH=TeslaCam         
        rclone mkdir onedrive:TeslaCam
        rclone lsd onedrive:
        

   You should see all the folders in your Onedrive after running the last command. I went ahead and created the 'TeslaCam' folder in my OneDrive outside of PowerShell

     11. Finally run `halt` to shut down the Pi and you are ready to connect to your car

        
         
  
  
