---
layout: post
title: Como verificar a integridade de arquivos baixados?
subtitle: E para que fazer isto?
tags: [powershell, checksum, hash]
comments: true
---

Você já deve ter notado que nas páginas de downloads de alguns sites são exibidas algumas sequências de letras e números chamadas de checksum ou hash.

O **checksum** serve para verificar se o download ocorreu sem que o arquivo tenha sido corrompido na transmissão ou se o arquivo foi de alguma forma modificado no site de origem. 

Mesmo uma pequena mudança no arquivo, irá gerar um valor de checksum diferente.

As versões mais recentes do Windows possuem um utilitário para verificação desse valor.

Por exemplo, ao baixar o arquivo abaixo, o checksum é: 

![Checksum](/assets/img/download-page-checksum.png){: .mx-auto.d-block :}

~~~
Checksum: 5787b180a60a8d52bc42ddb8c51884ca4263f5ed47dc10bb72229a49e8b07497
~~~

Para fazer o checksum, abra o PowerShell. Navegue para a mesma pasta onde está o arquivo e digite o comando abaixo:

~~~
certutil -hashfile SLE-15-SP1-Packages-x86_64-GM-DVD1.iso SHA256
~~~

Após alguns segundos, o resultado deve ser conforme a imagem abaixo:
![certutil](/assets/img/certutil.png){: .mx-auto.d-block :}

Note que o valor é igual ao informado no site.

Caso seja diferente, baixe o arquivo novamente pois, pode ter sido corrompido durante o download. Caso ocorra novamente, entre em contato com o site.

## Tipos de checksum

Os checksum mais comuns são MD5, SHA-1 ou SHA-2 (SHA256, SHA384, SHA512).
No exemplo acima, o checksum era SHA256, ou 256 bits, que divididos por 8, são 32 bytes. A família de criptografia SHA-2 utiliza duas funções de geram esse conjunto de carateres chamados de palavras. O resultado então são 64 caracteres.
