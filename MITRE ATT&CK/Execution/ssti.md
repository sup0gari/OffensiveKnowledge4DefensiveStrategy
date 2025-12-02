# SSTiとは
Server-Side Template Injectionの略で、Webアプリケーションの脆弱性の一種。
アプリケーションがユーザーから受け取った入力を、サーバー側で動作するテンプレートエンジンに安全でない形で渡した際に発生する。

## テンプレートの特定入力
`{{ 7*'7' }}` 49ならTwig(PHP), 7777777ならJinja2(Python)  
`${7*7}` 49ならFreemaker(Java)  
`#set($a = 7*7)$a` 49ならVelocity(Java)  
`${smarty.version}` バージョンが表示されたらSmarty(PHP)  
`<%= 7*7 %>` 49ならERB(Ruby)  
`__${7*7}__` 49ならThymeleaf(Java)  
`{{ this }}` 何らかのオブジェクトが返ればHandlebars(JavsScript)  
