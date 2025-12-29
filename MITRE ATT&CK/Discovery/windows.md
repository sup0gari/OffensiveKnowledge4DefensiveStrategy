## ユーザー情報
```bash
net user # すべてのユーザーを表示
net user <ユーザー名> # 指定したユーザー情報を表示
whoami /priv # 自身の権限を表示
cmdkey /list # 保存された資格情報を表示
```

## ファイル表示
```bash
Get-ChildItem -Force # すべてのファイルを表示
dir /a # cmd
```

## プロセス情報表示
```bash
Get-Process
ps
tasklist /v
netstat -ano
```

## 権限表示
```bash
icacls <ファイルまたはディレクトリ>
(I) # 親フォルダの設定がそのファイルに継承される。
(F) # フルコントロール
(RX) # 読み取りと実行
```

## サービス関連
```bash
sc.exe start <サービス>
sc.exe stop <サービス>
sc.exe query <サービス> # サービスの状態
sc.exe config <サービス> binPath="<パス>" # binPathの変更
sc.exe qc <サービス> # サービス詳細確認
```

## Active Directory関連
```bash
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName | Select Name, ServicePrincipalName # SPNを持つユーザー列挙
```
