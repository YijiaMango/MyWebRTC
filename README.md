## URL

entry: https://yijiamango.github.io/MyWebRTC/

channel:
```
https://yijiamango.github.io/MyWebRTC/321
```

每頻道畫面走 **該 port 的 signal zrok**（`yijiamango321…/live.jpg`），不再共用 5757。  
多 Client（digits→321/322…）各自 ShareZrok 後，入口快照才會分開。

TD：重載 `Signaling/signalingServer1/webserver1_callbacks`。
