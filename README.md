# autosend-photo-inha-line
use notify_line app send ipcam photo with home-assistant</br>
Install hacs { https://hacs.xyz/docs/configuration/basic }</br>
Apply for LINE API { https://notify-bot.line.me/zh_TW/ }</br>
Intell HA Line Notify (https://github.com/maxmacstn/HA-Line-Notify)</br>

add whitelist external dirs</br>
nano /config/configuration.yaml</br>
```
homeassistant:
  whitelist_external_dirs:
    - /media
```
Transfer to Home Assistant automation</br>
"Create a new automation to use the 'notify_line' app to send IPCam photos with Home Assistant.</br>
