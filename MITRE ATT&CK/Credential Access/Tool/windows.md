## DPAPI
DPAPIで暗号化されたファイルを復号するにはMasterkeyが必要で、`dir /S /AS`を使って探すことができる。  
`runas /savecred`、資格情報を記憶するにチェック、Outlookなどがパスワードを保存しているといった場合に下記のコマンドで探すことができる。
```powershell
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Vault # ブラウザの自動補完、アプリケーションが保存したパスワード
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Credentials # ローカル端末関連のパスワード
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Protect # 端末固有のデータのmasterkey
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Vault # あまり使われない
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Credentials # ドメインネットワーク内の共有フォルダのアクセス権や/savecredなどのデータ
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Protect # ユーザーごとのデータのmasterkey
```
