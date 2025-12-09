## 現在使用しているユーザー情報を表示  
`id`

## 権限昇格できる可能性のあるグループ
```bash
lxd # lxdコンテナ環境を利用し、ターゲットシステムのroot権限を奪取できる可能性あり。
```

## 存在するユーザーの表示
`cat /etc/passwd`

## カレントディレクトリの表示  
`pwd`

## ファイル情報を表示  
```bash
ls # ファイル一覧を表示
ls -la # ファイル一覧を権限も含めて表示
cat # ファイルの中身を表示
strings # ファイルの中身の文字列のみ表示
stat # ファイル統計を表示
```

## ポート情報を表示
```bash
ss # またはnetstat
-t # TCPのみ表示
-l # Listenポートのみ表示
-n # IPアドレスやポート番号を数値で表示
-p # プロセス名とPIDを表示
```

## 検索
```bash
find <検索場所のパス> <オプション> <検索ファイル名>
-group <グループ名>
-type <ファイル形式> # ファイルならf, ディレクトリならd
-name <検索したいワード>
-iname <検索したいワード> # 大文字小文字を区別しない
-perm -4000 # SUID
-perm -2000 # SGID
-user <ユーザー名>
-exec <コマンド> # 検索内容に対してコマンド実行した結果を表示
```

## SUID, SGID検索
```bash
find / -perm -4000 -type f -exec ls -l {} \; 2>/dev/null # SUID検索
find / -perm -2000 -type f -exec ls -l {} \; 2>/dev/null # SGID検索
```

## sudoers
一般ユーザーが sudo コマンドを使用する際に、どのコマンドを、どのユーザーの権限で、パスワードなしで実行できるかを細かく定義したファイル  
`/etc/sudoers`に通常あり、`sudo -l`で見れる。
