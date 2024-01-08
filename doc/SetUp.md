# Set Up SD Card

1. Download the [latest teslausb image](https://github.com/marcone/teslausb/releases) and a flashing/imaging tool. I used [Raspberry Pi Imager](https://github.com/marcone/teslausb/releases)

2. Attached SD card to computer and use imager to erase and format the card. Select Raspberry Pi Zero 2 W and scroll down under Operating System to find erase. Besure to select the correct storage device as this will erase all information on the drive. 

![rpiErase](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/8bbe9d88-2d48-4444-9df1-42df59b5b689)

3. After formatting the drive Under Operating System scoll down to Use custom and locate where you save the teslausb image. Selec the Storage drive you formatted in the previous step.

![rpiImage](https://github.com/kamelne/teslausb_OneDrive/assets/57120024/e9fdab14-c572-4480-a5bf-b914926ebf25)

4. Once the SD card has been imaged and verified, disconnect then reconnect it and you will see a new drive called "bootfs". Here you will replace the teslausb_setup_variables.conf file with the one I have attached and make a few edits using notepad or a text editor of your chouce.
