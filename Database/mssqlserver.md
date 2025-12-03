# Microsoft SQL Serverとは
マイクロソフトが開発したRDBMS

## ポート
1433

## impacket-mssqlclientを使用した接続
```bash
impacket-mssqlclient <ユーザー名>@<ターゲット> -windows-auth # -windows-authが不要な場合あり
impacket-mssqlclient <ユーザー名>:<パスワード>@<ターゲット> -windows-auth # -windows-authが不要な場合あり
impacket-mssqlclient -k <FQDN> # Kerberos認証
```

