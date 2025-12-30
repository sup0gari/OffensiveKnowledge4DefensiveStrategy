# impacket-psexecとは
MicrosoftのSysinternalsが提供するPsExecの機能を、Pythonのライブラリ（Samba/impacket）を使ってゼロから再実装したツール。  
Administratorの有効なパスワードが手に入れば、システムはそれが正規の管理者によるリモート操作であると認識し、アクセスを許可する。
SMB(445)が有効であればWinRMが有効でなくても使用できることがある。

## コマンド
```bash
impacket-psexec 'administrator:<パスワード>@<ターゲット>'
impacket-psexec administrator:'<パスワード>'@<ターゲット>
impacket-psexec administrator@<ターゲット> -hashes <NTLMハッシュ>
```
