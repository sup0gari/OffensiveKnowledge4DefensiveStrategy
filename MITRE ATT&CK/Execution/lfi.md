# LFIとは
攻撃者がWebアプリケーションに任意のローカルファイルを読み込ませ、そのファイルの内容をブラウザに表示させる脆弱性  
ディレクトリトラバーサルと似ている。

## 足掛かり
WebアプリがURLのパラメータからページを表示させている場合  
`test.com/index.php?page=english.html`  
pageパラメータに`../../../../windows/win.ini`や`../../../../etc/passwd`などを指定する。

## ドキュメントルートによくある機密ファイル
```bash
.env
.htaccess
.htpasswd
web.config
config.php
.git
```
