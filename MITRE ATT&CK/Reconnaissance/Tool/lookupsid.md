# lookupsidとは
Impacketに含まれるPythonスクリプトで、msrpc経由でSIDをブルートフォースし、ユーザー名やグループを列挙するツール。  
lookupsidを実行する際にrpcを使用して通信するため、匿名のrpc通信が可能であれば使用できる可能性が高い。

## コマンド
```bash
impacket-lookupsid <ユーザー名>@<ターゲット> -no-pass
impacket-lookupsid <ユーザー名>@<ターゲット> -no-pass | grep 'SidTypeUser' | sed 's/.*\\\(.*\) (SidTypeUser)/\1/' > users.txt # SidTypeUserだけを抜き出し、users.txtに保存。
impacket-lookupsid <ユーザー名>:<パスワード>@<ターゲット> # 認証あり
```
