If you insert a file named dlc_cfg.txt into your SD card, place the SD card into the MKS DLC32 board, and then power it on, the program will initialize and read the SD card. If it finds the dlc_cfg.txt file, it will process its contents.

https://github.com/makerbase-mks/MKS-DLC32-FIRMWARE/blob/main/Firmware/Grbl_Esp32/src/mks/MKS_updata.cpp

When examining the code in the file Grbl_esp32 > src > mks > Mks_updata.cpp, you can find specific conditions that determine how the program handles the configuration file:

cpp
Copy
void mks_cfg_find(void) {
    String p;
    char send_data[128];

    p = tf.readFileLine(CFG_FILE_PATG, mks_updata.updata_line);
    if ((strstr(p.c_str(), "-") == NULL) 
        && (strstr(p.c_str(), "/*") == NULL) 
        && (strstr(p.c_str(), "*-") == NULL) 
        && (strstr(p.c_str(), "//") == NULL)
        && (p.length() < 127)) 
    {   
        if ((strstr(p.c_str(), "=") != NULL)) {
            mks_updata.is_have_data_ud = true;
        } else if (strstr(p.c_str(), "[ESP110]") != NULL) {
            mks_updata.is_have_data_ud = true;
        } else if (strstr(p.c_str(), "[ESP100]") != NULL) {
            mks_updata.is_have_data_ud = true;
        } else if (strstr(p.c_str(), "[ESP101]") != NULL) {
            mks_updata.is_have_data_ud = true;
        } else if (strstr(p.c_str(), "[ESP131]") != NULL) {
            mks_updata.is_have_data_ud = true;
        } else {
            mks_updata.is_have_data_ud = false;
        }
    }
}
This code ensures that a line is ignored if it contains any of the following characters: -, /*, *-, //, or if the line exceeds 127 characters.

A line is accepted if it contains one of the following: =, [ESP110], [ESP100], [ESP101], or [ESP131].

Initially, when I tried to configure the system, I added [ESP115]ON to activate Wi-Fi. However, after reviewing this code, I realized that only the specific commands listed above are accepted. This explains why my router named "TIM-32883215" was not connecting via the SD card configuration. After investigating, I discovered that the program only processes the predefined commands.

Therefore, I recommend not changing or adding anything outside the accepted parameters.

Finally, if the program successfully finds and updates any parameters, it will rename dlc_cfg.txt to bkg_cfg.txt. This renaming indicates that the update process was successful. If the file name remains dlc_cfg.txt, it means an error occurred, and no updates were applied.

This method allows you to verify whether the configuration update worked. If the file name changes to bkg_cfg.txt, the process was successful. If not, an error likely occurred, and no changes were made.

[MSG:Start mDNS with hostname:http://grblesp.local/]

This firmware:

[https://github.com/makerbase-mks/MKS-DLC32/tree/main/MKS-DLC32-main/firmware/TS35/Laser/Normal/Board_V2.0/V2.0.8_H35_20211222_N.bin](https://github.com/makerbase-mks/MKS-DLC32/blob/main/MKS-DLC32-main/firmware/TS35/Laser/Normal/Board_V2.0/V2.0.8_H35_20211222_N.bin)

C:\Users\****\MKS-DLC32-main\MKS-DLC32-main\firmware\TS35\Laser\Normal\Board_V2.0\V2.0.8_H35_20211222_ON.bin

---------------------------------------------------------------------------------------------------

Link for document https://github.com/makerbase-mks/MKS-DLC32/blob/main/MKS-DLC32-main/doc/DLC32%20wiring%20manual.pdf

![image](https://github.com/user-attachments/assets/200ae15f-8bfc-4819-82d0-b92283e1092c)




