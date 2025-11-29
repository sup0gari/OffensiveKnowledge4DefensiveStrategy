# WinRMとは
主にWindows環境で、リモートのコンピューターを管理するために設計された管理プロトコル。標準的なWebプロトコルであるHTTPとHTTPSを利用して通信します。

## ポート
5985(HTTP)
5986(HTTPS)

## 接続方法（evil-winrmを使用）
```bash
evil-winrm -i <ターゲット> -u <ユーザー名> -p '<パスワード>' # パスワードで接続
evil-winrm -i <ターゲット> -u <ユーザー名> -H '<NTハッシュ>' # NTハッシュで接続
```
