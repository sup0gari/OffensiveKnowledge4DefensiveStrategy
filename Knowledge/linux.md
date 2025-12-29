## TTYシェルの確立
リバースシェルで獲得したシェルが不安定な場合、TTYシェルを確立することで安定したインタラクティブなシェルが得られる。  
`python3 -c "import pty;pty.spawn('/bin/sh')"`  
python3が使えないとき
```bash
script /dev/null -c bash # PTYという疑似端末の割り当て
CTRL + Z # バックグラウンド
stty raw -echo # 端末側の文字をそのまま送るようにする。TabやCTRL + Cが使えるようになる可能性がある
fg # foregroundの略。バックグラウンドから戻る
export TERM=xterm
```

## ブラウザでドメインの名前解決ができないとき
`echo <ターゲット> <ドメイン> | sudo tee -a /etc/hosts`

## シェル
```
sudo su - # rootシェル
sudo -i # rootシェル
sudo -u <ユーザー名> <コマンド> # 指定したユーザーとしてコマンド実行
```

## 任意のファイルをHTTP経由で配布(python3を使用)
```bash
python3 -m http.server 8000 # 任意のファイルがあるディレクトリで実行
```

## URLからファイルをダウンロード
```bash
wget <URL>
curl <URL> -o <保存名>
```

## SUID, SGIDとは
一般ユーザーが実行するプログラムに対し、一時的にプログラムの所有者や所有グループの権限を与えることで、システム管理を効率的に行うために設計されている。  
`-rwsr-xr--`このようにパーミッションにsが付く。
```bash
find / -perm -4000 -type f -exec ls -l {} \; 2>/dev/null # SUID検索
find / -perm -2000 -type f -exec ls -l {} \; 2>/dev/null # SGID検索
```

## cat EOFを使ったファイル作成
```bash
cat << EOF > test.sh
#!/bin/bash
echo "Hello World!"
EOF
```

## 環境変数の書き換え
```bash
export PATH=<書き換えたいパス>
```

## ssh関連
秘密鍵のファイル名  
`id_rsa`, `id_dsa`, `id_ed25519`  
公開鍵のファイル名  
`id_rsa.pub`, `id_dsa.pub`, `id_ed25519.pub`  
ファイルパス  
`/home/<ユーザー名>/.ssh/`  
公開鍵登録パス  
`/home/<ユーザー名>/.ssh/authorized_keys`

## adm
システムのログファイルを読み取る権限を持つユーザー。  
`/var/log`配下のファイルを閲覧可能。

## 一時ファイルの作成と移動
`cd $(mktemp -d)`

## 16進数をasciiに変換
`xxd -r -p <ファイル> > <ASCII>`

## sshエラー
```bash
no mutual signature supported # 署名ルールが一致しないときのエラー
-o PubkeyAcceptedKeyTypes=ssh-rsa # ssh-rsa(sha1)を強制的に使用
```

## パラメータのバイパス
```bash
${IFS} # スペース
echo<base64 ペイロード>|base64 -d|bash
echo -n <ペイロード> | base64 -d # -n入れたほうがいい
```
