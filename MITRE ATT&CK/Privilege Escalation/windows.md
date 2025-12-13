# Server Operatorsを悪用した権限昇格
VSS(Volume Shadow Copy Service)という標準的なWindowsサービスをターゲットに、binPath(サービス起動時に実行するプログラム)を書き換える。  
VSSサービスは通常、SYSTEMアカウントの権限で実行されるため権限昇格が可能。
```bash

```
