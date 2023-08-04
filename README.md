# autosend-photo-inha-line
use notify_line app send ipcam photo with home-assistant</br>
Install hacs { https://hacs.xyz/docs/configuration/basic }</br>
Apply for LINE API { https://notify-bot.line.me/zh_TW/ }</br>
Install HA Line Notify (https://github.com/maxmacstn/HA-Line-Notify)</br>

add whitelist external dirs</br>
nano /config/configuration.yaml</br>
```
homeassistant:
  whitelist_external_dirs:
    - /media
```
Transfer to Home Assistant automation</br>
"Create a new automation to use the 'notify_line' app to send IPCam photos with Home Assistant.</br>
Click on the three dots in the upper right corner, choose "Edit as YAML," </br>

```
alias: Gate view
description: 車庫人形偵測
trigger:
  - platform: state
    entity_id:
      - binary_sensor.gate_cell_motion_detection
    for:
      hours: 0
      minutes: 0
      seconds: 3
    to: "on"
    from: "off"
condition: []
action:
  - service: camera.snapshot
    data:
      entity_id: camera.gate
      filename: /media/{{ now().strftime('%Y%m%d%H%M%S') }}.jpeg
  - service: notify.line_notification
    data:
      message: Gate camera:移動偵測已達3秒，附上實況照
      data:
        file: /media/{{ now().strftime('%Y%m%d%H%M%S') }}.jpeg
mode: single
```
