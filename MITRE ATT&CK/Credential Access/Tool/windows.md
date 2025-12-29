## DPAPI
DPAPIで暗号化されたファイルを復号するにはMasterkeyが必要で、`dir /S /AS`を使って探すことができる。  
`runas /savecred`、資格情報を記憶するにチェック、Outlookなどがパスワードを保存しているといった場合に下記のコマンドで探すことができる。
```powershell
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Vault
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Credentials
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Protect
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Vault
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Credentials
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Protect
```
