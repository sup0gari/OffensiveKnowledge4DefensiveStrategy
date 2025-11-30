## TTYシェルの確立
リバースシェルで獲得したシェルが不安定な場合、TTYシェルを確立することで安定したインタラクティブなシェルが得られる。  
`python3 -c "import pty;pty.spawn('/bin/sh')"`
