# ftpとは
File Transfer Protocol（ファイル転送プロトコル）の略称で、インターネット上でファイルをやり取りするためのプロトコル。平文でデータを転送。

## ポート
21

## 接続方法
```bash
ftp <ターゲット>
```

## コマンド
```bash
help # 使用できるコマンドを表示
get # 指定したファイルをダウンロード
put # 指定したファイルをアップロード
binary # バイナリファイルを転送する場合に使用
ascii # OS間の改行コードを自動的に変換し、テキストファイルを転送する場合に使用
passive # アウトバウンド接続を確立
```

## 脆弱性
匿名によるアクセスを許可している場合は以下の認証情報でログインできることがある。
```bash
ftp 10.10.10.1

Connected to 10.129.1.14.
220 (vsFTPd 3.0.3)
Name (10.129.1.14:kali): anonymous
331 Please specify the password.
Password: # 空でEnter
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> 
```
