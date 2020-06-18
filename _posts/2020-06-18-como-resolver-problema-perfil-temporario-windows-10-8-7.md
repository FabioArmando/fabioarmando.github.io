---
layout: post
title: Como resolver problema com perfil temporário no Windows 10, 8 e 7.
tags: [windows, usuários, prefil]
comments: true
---

Um dos problemas que os usuários costumam encontrar é uma mensagem informando que você está logado com um perfil temporário no Windows 10, 8 e Windows 7 com texto "Não é possível acessar os arquivos. Os arquivos criados no perfil serão excluídos depois que você sair. Para corrigir isso, saia e tente entrar mais tarde."

![Tela de aviso perfil temporário Windows](/assets/img/perfil-temporario-windows-10.jpg){: .mx-auto.d-block :}

Explico neste passo-a-passo uma maneira de resolver em 5 passos:

## Passo 1: Iniciar o editor de registro (Registry Editor)

Para começar, para todas os passos, você precisará ter uma conta de administrador. Se antes do erro "Você está logado com um perfil temporário" sua conta tinha já tinha esse direito, ela permance com esse acesso e então você pode continuar. Quando um computador é utilizado por toda a família com uma única conta, normalmente já possui perfil de administrador.

Se você tinha uma conta de usuário simples, precisará executar estes passos em outra conta (administrador) ou entrar em modo de segurança com suporte à linha de comando, ativar a conta de administrador oculta e executar todas as ações nela.

Inicie o editor de registro (pressione as teclas Win + R, digite **regedit** e pressione Enter).

![Executar o regedit](/assets/img/run-regedit.png){: .mx-auto.d-block :}

## Passo 2: Encontre o ProfileList

Vá expandindo a seleção à esquerda até o caminho abaixo 

~~~
HKEY_LOCAL_MACHINE \ SOFTWARE \ Microsoft \ Windows NT \ CurrentVersion \ ProfileList
~~~

Observe a presença de uma sucessão com um ".bak" no final, selecione-o.

![Regedit profile com .bak](/assets/img/regedit-profile-bak.png){: .mx-auto.d-block :}

## Passo 3: Encontre o ProfileImagePath

À esquerda, verifique se o valor em ProfileImagePath se o valor é o mesmo do nome do usuário em C:\Users (ou C:\Usuário).

## Passo 4: Caso o nome da pasta não seja o mesmo do usuário

Clique duas vezes no valor ProfileImagePath e altere-o para que ele tenha o caminho da pasta correta.

Se as seções à esquerda tiverem exatamente o mesmo nome que o atual, mas sem .bak, clique com o botão direito do mouse e selecione "Excluir".

Clique com o botão direito do mouse na seção com .bak no final, selecione "Renomear" e remova .bak.

Feche o editor de registro, reinicie o computador e tente iniciar com o perfil em que ocorreu um erro.

## Passo 5: Caso o nome do caminho da pasta em ProfileImagePath esteja correto

Caso no lado esquerdo do editor de registro houver uma seção com o mesmo nome (todos os números são iguais) e com ".bak" no final, clique com o botão direito do mouse e selecione "Excluir". Confirme a exclusão.

Clique com o botão direito do mouse na seção com .bak e também a exclua.

Reinicie o computador e tente novamente fazer login na conta danificada - os dados no registro deverão ser recriados automaticamente.
