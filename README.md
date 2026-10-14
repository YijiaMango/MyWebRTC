## 網址

<https://yijiamango.github.io/MyWebRTC/>

## 用途

GitHub Pages 靜態跳板：收 TouchDesigner WebRTC 畫面，並把手機 DeviceOrientation / DeviceMotion 經 DataChannel `OscData` 送回 TD → `oscout_signal`。

不含 MediaPipe / 鏡頭姿態。

## 通道號 = TD Port（多路同步）

URL 的 `port` **永遠跟 TD COMP 的 Port 相同**（Client_1 → 321、Client_2 → 322…）。

| 場景 | URL | 實際 WebSocket |
|------|-----|----------------|
| 本機 / 同網 | `http://TD_IP:5757/?port=321` | `ws://TD_IP:321` |
| GitHub Pages + tunnel | `?ws=xxx.trycloudflare.com&port=321` | `wss://xxx:443`（443 僅傳輸層；邏輯通道仍是 321） |

多通道管理就記 TD 號碼即可，不必記 443。

```text
https://yijiamango.github.io/MyWebRTC/?ws=你的tunnel&port=321
https://yijiamango.github.io/MyWebRTC/?ws=你的tunnel&port=322
```

每個 TD Client 各自打一條 `cloudflared tunnel --url http://127.0.0.1:32N`。

## OSC（Client oscout）

| Address | Args |
|---------|------|
| `/webrtc/pose` | alpha beta gamma |
| `/webrtc/pose/absolute` | 0\|1 |
| `/webrtc/accel` | x y z |
| `/webrtc/accelg` | x y z |
| `/webrtc/rotrate` | alpha beta gamma |

## Query

| Param | 說明 |
|-------|------|
| `ws` | tunnel / signaling 主機（GH Pages 必填） |
| `port` | **TD 通道號**（與 COMP Port 同步） |
| `wsp` | 罕見：強制 dial 埠（預設 tunnel=443、區網=port） |
| `osc=0` | 關閉姿態→OSC |
| `signalHud=1` | TD→Web JSON 浮層 |

## 同源檔

`Dat/Qin_project/WebRTC_Client_1/WebServer/web_index.html` → 同步本目錄 `index.html` 再推 GitHub。
