## 網址

<https://yijiamango.github.io/MyWebRTC/>

## 用途

GitHub Pages 靜態跳板：收 TouchDesigner WebRTC 畫面，並把手機 **DeviceOrientation / DeviceMotion** 經 DataChannel `OscData` 送回 TD，再由 Client `oscout_signal` 轉成區域 OSC。

不含 MediaPipe / 鏡頭姿態。

## 連線

1. TD 開好 Signaling（建議用 Cloudflare Tunnel / ngrok 打出 **WSS**）
2. 手機開：

```text
https://yijiamango.github.io/MyWebRTC/?ws=你的tunnel主機&port=443
```

3. iOS 先點「啟用姿態感測 → OSC」授權
4. TD Client `oscout_signal` 會送出：

| Address | Args |
|---------|------|
| `/webrtc/pose` | alpha beta gamma |
| `/webrtc/pose/absolute` | 0\|1 |
| `/webrtc/accel` | x y z |
| `/webrtc/accelg` | x y z |
| `/webrtc/rotrate` | alpha beta gamma |

自訂訊息也可在 JSON 裡帶 `msgs: [["/foo",[1,2]]]`。

## Query

| Param | 說明 |
|-------|------|
| `ws` | Signaling 主機（GH Pages **必填**） |
| `port` | Signaling 埠（GH Pages 通常 `443`） |
| `osc=0` | 關閉姿態→OSC |
| `signalHud=1` | 顯示 TD→Web JSON 浮層 |

## 同源檔

TD 本機 WebServer 同源：`Dat/Qin_project/WebRTC_Client_1/WebServer/web_index.html`  
改完請同步覆蓋本目錄 `index.html` 再推 GitHub。
