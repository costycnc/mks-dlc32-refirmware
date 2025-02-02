If insert dlc_cfg.txt in your sdcard, and insert sdcard in mks dlc32 board and after insert power, at init the program will be read the sdcard and if find dlc_cfg.txt, but … 

If watch the code in file Grbl_esp32>src>mks>Mks_updata.cpp find here some conditions:

void mks_cfg_find(void) {
    String p;
    char send_data[128];

    p = tf.readFileLine(CFG_FILE_PATG, mks_updata.updata_line);
    if( (strstr(p.c_str() ,"-") == NULL) 
         && (strstr(p.c_str() ,"/*") == NULL) 
         && (strstr(p.c_str() ,"*-") == NULL) 
         && (strstr(p.c_str() ,"//") == NULL)
         && (p.length() < 127) 
        )  
    {   
        if( (strstr(p.c_str() ,"=") != NULL)) {
            mks_updata.is_have_data_ud = true;
        }else if(strstr(p.c_str() ,"[ESP110]") != NULL) {
            mks_updata.is_have_data_ud = true;
        }else if(strstr(p.c_str() ,"[ESP100]") != NULL) {
            mks_updata.is_have_data_ud = true;
        }else if(strstr(p.c_str() ,"[ESP101]") != NULL) {
            mks_updata.is_have_data_ud = true;
        }else if(strstr(p.c_str() ,"[ESP131]") != NULL) {
            mks_updata.is_have_data_ud = true;
        }else {
            mks_updata.is_have_data_ud = false;
        }
    }

This code did that the line is ommited if command contain one of these characters - , /* , _ , // and line not more as 127 characters

And a line is accepted if have one of this = , [ESP110], [ESP100], [ESP101] and [ESP131] 

Also when maked probe ,first to find this, i put [ESP115]ON for activate wifi , but after find this code i understand that accepted only these commands!

In my case the my router have name "TIM-32883215" and because not understand because not connect over sdcard i search myself and after find this i understand!

For this i raccomended don not change or add anything!

And finally if any parameters is find and changed by program the title of the dlc_cfg.txt will be changed in bkg_cfg.txt

In this mode will see that this metod working for you.If name dlc_cfg.txt is not changed seem that happen a error and anything is update!

[MSG:Start mDNS with hostname:http://grblesp.local/]

This firmware:

[https://github.com/makerbase-mks/MKS-DLC32/tree/main/MKS-DLC32-main/firmware/TS35/Laser/Normal/Board_V2.0/V2.0.8_H35_20211222_N.bin](https://github.com/makerbase-mks/MKS-DLC32/blob/main/MKS-DLC32-main/firmware/TS35/Laser/Normal/Board_V2.0/V2.0.8_H35_20211222_N.bin)

C:\Users\****\MKS-DLC32-main\MKS-DLC32-main\firmware\TS35\Laser\Normal\Board_V2.0\V2.0.8_H35_20211222_ON.bin

![image](https://github.com/user-attachments/assets/200ae15f-8bfc-4819-82d0-b92283e1092c)




