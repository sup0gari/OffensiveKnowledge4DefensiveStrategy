# windapsearchとは
Windowsドメイン内のユーザー、グループ、コンピュータ情報をLDAPクエリを使って列挙するためのPythonスクリプト

## コマンド例
```bash
windapsearch -d <ドメイン> --dc-ip <ターゲット> -U # 匿名バインド
windapsearch -d <ドメイン> --dc-ip <ターゲット> -U --custom "classObject=*"
windapsearch -d <ドメイン> --dc-ip <ターゲット> -U --admin-objects
windapsearch -m "Remote Management Users" -d<ドメイン> --dc-ip <ターゲット> -U # WinRMグループ検索
windapsearch -d <ドメイン> --dc-ip <ターゲット> -U --full
windapsearch --admin-objects -d <ドメイン> --dc-ip <ターゲット> -u '<ユーザー名>' -p '<パスワード>' # 認証ありバインド
windapsearch -m "Remote Management Users" -d <ドメイン> --dc-ip <ターゲット> -u '<ユーザー名>' -p '<パスワード>'
-U # 匿名バインド
-u # ユーザー名
-p # パスワード
```
