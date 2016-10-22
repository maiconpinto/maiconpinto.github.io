---
layout: post
title:  "Meu Ambiente de desenvolvimento!"
date:   2016-10-14 22:07:00 -0300
categories: blog
resume: 
---

## Meu Ambiente de Desenvolvimento

Recentemente tive que formatar meu notebook, e acabei procurando por um tutorial fácil e simples para configurar meu ambiente de desenvolvimento, de novo. 

Pesquisando, encontrei [este vídeo](https://www.youtube.com/watch?v=Q2N5blJ4VIo) do [Vedovelli](http://www.vedovelli.com.br/), que é um dos caras feras na web.

Abaixo segue a lista de comandos que foram utilizados no tutorial: 

###### Atualização

> sudo apt-get update

Atualiza a lista de repositórios por padrão.

###### Nginx

> sudo apt-get install nginx

Instala o servidor web, neste caso em substituição ao Apache. 

Para testar abra o navegador e digite http://localhost, deve aparecer uma mensagem "Welcome to nginx!".

![Welcome to nginx](/images/posts/001-welcome-to-nginx.png)

###### MySQL

> sudo apt-get install mysql-server

Instala o banco de dados MySQL, e no meio pede para digitar a senha do usuário root. Informe uma senha e prossiga. 

Para testar abra o terminal digite "mysql -uroot -p", ele vai pedir a senha que você informou um pouco antes, digite, e deve aparecer "mysql>".

> mysql_secure_installation

Configura alguns ajustes na segurança do mysql.

###### PHP 

> sudo apt-get install php7.0-fpm

> sudo apt-get install php7.0-mysql

> sudo apt-get install php7.0-mcrypt

Instalação do PHP. 

###### SublimeText3 (http://sublimetext.com/3)

> cd ~/Downloads 

> wget https://download.sublimetext.com/sublime-text_build-3126_amd64.deb

> sudo dpkg -i sublime-text_build-3126_amd64.deb

O Vídeo mostra de outra forma para fazer a instalação do SublimeText, está é uma adaptação minha.  

###### php.ini

> sudo subl /etc/php/7.0/fpm/php.ini

Trocar **;cgi.fix_pathinfo=1** por **cgi.fix_pathinfo=0**.

Segundo o vídeo, esta alteração é para que o PHP trabalhe bem com o nginx.

###### hosts

> sudo subl /etc/hosts

Neste arquivo é possível adicionar novas entradas, para apontar para o servidor nginx. No caso **teste.app**. 

*[...]*

Eu continuo outra hora aqui. 

*[...]*

> sudo apt-get install git

> sudo apt-get install nodejs

> sudo apt-get install npm


Abaixo o vídeo...

<div class="video-container">
	<iframe width="560" height="315" src="https://www.youtube.com/embed/Q2N5blJ4VIo" frameborder="0" allowfullscreen></iframe>
</div>