# ftpとは
File Transfer Protocol（ファイル転送プロトコル）の略称で、インターネット上でファイルをやり取りするためのプロトコル。平文でデータを転送

## ポート
21

## 接続方法
```bash
ftp <ターゲット>
```

## 例
```bash
ftp 10.10.10.1
```

## 脆弱性
匿名によるアクセスを許可している場合は以下の認証情報でログインできることがある。
```bash
ftp 10.10.10.1

# 以下出力例
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
