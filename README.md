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
"Create a new automation to use the 'notify_line' app to send IPCam photos with Home Assistant</br>
</br>
Click on the three dots in the upper right corner, choose "Edit as YAML," </br>
entity_id: Choose the motion detection sensor and IP camera</br>
My example is binary_sensor.gate_cell_motion_detection and camera.gate</br>

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
When motion detection reaches 3 seconds, Line will send a notification and receive a live photo stream.</br></br></br>
中文說明:</br>
添加完白名單後</br>
設定 > 裝置與服務 > 右下新增整合 > 輸入：onvif (添加 ipcam) </br>
移到 Home Assistant 自動化</br>
創建一個新的自動化，以使用“notify_line”應用程序通過 Home Assistant 發送實況照片</br>
單擊右上角的三個點，選擇“編輯 為 YAML”</br>
entity_id：選擇運動檢測傳感器， ipcam鏡頭</br>
我的範例是 binary_sensor.gate_cell_motion_detection 跟 camera.gate</br>
當運動檢測達到 3 秒時，Line 將發送通知跟照片</br>
傳感器 跟 鏡頭 要選對
