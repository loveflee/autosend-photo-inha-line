# autosend-photo-inha-line
use notify_line app send ipcam photo with home-assistant</br>
Install hacs { https://hacs.xyz/docs/configuration/basic }</br>
Apply for LINE API { https://notify-bot.line.me/zh_TW/ }</br>
Intell HA Line Notify (https://github.com/maxmacstn/HA-Line-Notify)</br>

add whitelist_external_dirs</br>
nano /config/configuration.yaml</br>
'''
homeassistant:</br>
  whitelist_external_dirs:</br>
    - /media</br>
'''
