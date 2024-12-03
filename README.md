help https://github.com/bdring/Grbl_Esp32/wiki
          $ESP100=xxxxxx  (your name router home)
          $ESP101=xxxxxx  (Your password router home)
          $ESP110=STA (Set/Get radio state which can be STA(router), AP(local), BT, OFF)
          $ESP115=ON
# mks-dlc2-refirmware
Firmare for costycnc foam cutter machine

In general , my clients are unexpert and principiants so when some client decided to change the arduino nano cnc shield v4 with mks dlc32 wifi shield , at official https://github.com/makerbase-mks/MKS-DLC32 address have many option and user not understand what version of firmware upload to wifi shield.
Anyway ,any firmware have is own caracteristic , for example if user ude a display , need to upload to wifi module the respective firmware for display that have.
But i suppose that client not have display (have only board without display) and want only to refirmware the cnc module, in this case i put here a basic firmware that mks raccomand!
<hr>

all grbl mks dlc32 esp commands https://github.com/costycnc/esp32-micropython-with-mks-dlc32-board-costycnc/blob/main/Commands.txt

==================================================================
==================================================================
costycnc foam cutter  https://www.costycnc.it
I inspired from here https://github.com/makerbase-mks/MKS-DLC32/issues/12

          when buy a new mks-dlc32  the wifi is OFF... so ... is not available on wifi networks window,
          so you can comunicate with mks dlc only serial.

          So open a serial terminal , connect with mks dlc over serial port and send 
          $ESP115=ON
          And receive a message like this:
          [MSG:Local access point ESPWIFI_47276 started, 192.168.4.1]
          [MSG:HTTP Started]
          [MSG:TELNET Started 8080]
          Now wifi is active and in default is in AP mode
          So ... if open wifi networks windows in your pc will see ESPWIFI_47276
          connect with this wifi , the default password is 12345678
          if webui page is not open automatically after connect
          write in browser 192.168.4.1
          
If want connect to your router at home 

          Insert these commands over serial:
          $ESP100=xxxxxx  (your name router home)
          $ESP101=xxxxxx  (Your password router home)
          $ESP110=STA (Set/Get radio state which can be STA, AP, BT, OFF)
          $ESP115=ON
          And will receive:
          [MSG:Client Started]
          [MSG:Connecting TIM-32883215]
          [MSG:Connecting.]
          [MSG:Connecting..]
          [MSG:Connecting...]
          [MSG:Connecting....]
          [MSG:Connecting.]
          [MSG:Connecting..]
          [MSG:Connecting...]
          [MSG:Connecting....]
          [MSG:Connecting.]
          [MSG:Connecting..]
          [MSG:Connecting...]
          [MSG:Start mDNS with hostname:http://mks_grbl.local/]
          [MSG:HTTP Started]
          [MSG:TELNET Started 8080]
          ok
          so... write in browser http://mks_grbl.local/ and webui will open



