# Set Up Raspberry PI
There are four phases to setting up the Pi:
1. Get the OS onto the micro sd card.
2. Get a shell on the Pi.
3. Set up the archive for dashcam clips.
4. Set up the USB storage functionality.

### Get OS on SD Card
1. Download the [latest teslausb image](https://github.com/marcone/teslausb/releases) and a flashing/imaging tool. I used [Raspberry Pi Imager](https://github.com/marcone/teslausb/releases)

2. Attached SD card to computer and use imager to erase and format the card. Select Raspberry Pi Zero 2 W and scroll down under Operating System to find erase. Besure to select the correct storage device as this will erase all information on the drive. 

![rpiErase](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/8bbe9d88-2d48-4444-9df1-42df59b5b689)

3. After formatting the drive Under Operating System scoll down to Use custom and locate where you save the teslausb image. Selec the Storage drive you formatted in the previous step.

![rpiImage](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/e9fdab14-c572-4480-a5bf-b914926ebf25)

4. Once the SD card has been imaged and verified, disconnect then reconnect it and you will see a new drive called "bootfs". Here you will replace the teslausb_setup_variables.conf file with the one I have attached and make a few edits using notepad or a text editor of your chouce.

[sample setup variables](doc/teslausb_setup_variables.conf)

- The changes I made are to comment out the use of CIFS and uncomment rclone archiving

![addrclone](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/cb4c6846-9bed-4f45-80da-c4338b0e27c4)

  
- Choose Partition Sizing, I choose to allocate 95% of the drive for Camera storage and 5% for Music. You can change these number if you plan on having music on your drive.

![partitionsizing](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/ae6a730a-4537-4782-a63a-6e8565cf17ef)

- Set Wifi SSID and Password, replace everything within the quotes with you SSID and Password

![ssid](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/6753560b-2b1d-4d0b-ae64-908ab858bf91)

- Use ExFat filesystem, might not be necessary but my SD card was also in ExFat format

![exfat](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/f580a8b8-e777-466f-8df5-6b05f4e0f865)

