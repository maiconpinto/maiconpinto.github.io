---
layout: post
title:  "Meu Ambiente de desenvolvimento!"
date:   2016-10-14 22:07:00 -0300
categories: blog
resume: Recentemente tive que formatar meu notebook, e acabei procurando por um tutorial fácil e simples para configurar meu ambiente de desenvolvimento, de novo. 
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

![Welcome to nginx](/images/posts/001-welcome-to-nginx.png){: .responsive-img}

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

> sudo apt-get install php7.0-intl // Para o CakePHP

> sudo apt-get install php7.0-mbstring // Para o CakePHP

Instalação do PHP. 

###### SublimeText3 (http://sublimetext.com/3)

> cd ~/Downloads 

> wget https://download.sublimetext.com/sublime-text_build-3126_amd64.deb

> sudo dpkg -i sublime-text_build-3126_amd64.deb

O Vídeo mostra de outra forma para fazer a instalação do SublimeText, esta é uma adaptação minha.  

###### php.ini

> sudo subl /etc/php/7.0/fpm/php.ini

Trocar **;cgi.fix_pathinfo=1** por **cgi.fix_pathinfo=0**.

Segundo o vídeo, esta alteração é para que o PHP trabalhe bem com o nginx.

###### hosts

> sudo subl /etc/hosts

Digite **127.0.1.1 teste.app** logo abaixo do 127.0.1.1 localhost. O arquivo irá ficar assim:


> 127.0.0.1	localhost
>
> 127.0.1.1 teste.app

Neste momento, foi criado um apontamento de **teste.app** para o servidor nginx que está instalado localmente. Então, se você acessar **htpp://localhost** ou **htpp://teste.app**, quem irá responder por estes endereços é o nosso servidor web nginx. Porém, ainda não configuramos o nginx para que ele responda com os arquivos deste projeto **teste.app**.

###### Configuração do nginx

Dentro do diretório **/etc/nginx** existem duas pastas que interessam: **sites-available** e **sites-enabled**. Uma configuração só é válida, quando estiver em **sites-enabled**. Mas para isso vamos configurar em **sites-available**. 

> sudo subl /etc/nginx/sites-available/teste.app

Digite a seguinte configuração: 

{% gist 135c2eb943bb0a2eaf1922425fc44302 %}

Esta configuração não é exatamente a que está no vídeo, mas serve para exemplo. Eu não quero seguir como no vídeo, e criar links simbólicos apontando para "FODER_HERE". 

O que eu quero é criar meus projetos dentro de **/var/www/** seguindo uma convenção **projeto.local**, assim, quando eu estiver trabalhando com meu site, por exemplo, *maiconpinto.com.br*, eu terei **maiconpinto.com.br.local**. Parece ruim isso, mas é só uma convenção, assim como o Vedovelli usa projeto.app eu vou usar projeto.local. 

###### Testando teste.app

Continuando com o vídeo, próximo passo é criar o arquivo index.php:

> sudo subl /var/www/teste.app/index.php

E digitar apenas:

> `<?php echo phpinfo(); ?>`

Como o Vedovelli explica muito bem, não basta apenas isso, é preciso ativá-lo, criando o link simbólico para **/etc/nginx/sites-enabled/**.

> sudo ln -s /etc/nginx/sites-available/teste.app /etc/nginx/sites-enabled/

Reiniciar os serviços nginx e o php7.0-fpm:

> sudo service nginx restart
> 
> sudo service php7.0-fpm restart

Acessando http://teste.app irá visualizar o resultado de phpinfo(), que é a tela de configuração semelhante a essa abaixo.

![phpinfo()](/images/posts/002-phpinfo.png){: .responsive-img}

Se a tela acima aparecer para você, é que tudo estará ok\*. 

\* *#SQN, ainda faltam coisas*

###### Comandos extras

Durante a instalação eu tive alguns problemas, pois no vídeo é instalado o php5, e no meu caso instalei o php7. Porém não é só isso, eu **nunca** tinha instalado o servidor web Nginx, então para mim isso foi um desafio. Apesar do vídeo explicar bem, e só seguir o passo-a-passo, mesmo assim sempre dá algum problema. Por isso, resolvi postar estes comandos extras que me ajudaram a resolver algum problema. 

> sudo nginx -t

Este comando me ajudou muito para saber quando estava configurando virtual hosts com algum erro, como duplicar **server_name**. Por isso achei importante compartilhar ele.

> sudo chown -R $USER:$USER /var/www/teste.app

Este comando altera as permissões para o usuário atual. Permissões é uma questão muito complicada no linux, pois é bem comum dar problemas por causa delas. Seu usuário do linux não tem permissão para criar pastas no **/var/www/**, por exemplo, então você precisa utilizar o **sudo** na frente, que ele vai criar com as permissões de **root**. Só que mesmo criando as pastas ficaria impossível de salvar os arquivos dentro delas, pois pertence ao usuário **root**. Para corrigir isso, basta executar o comando acima, utilizando o seu usuário, e não root.

###### Ativando PHP modules

No vídeo do Vedovelli, ele ativa módulos PHP para utilizar com Laravel, eu não uso Laravel por enquanto, mas não custa executar mais estes comandos.

> phpenmod mcrypt
>
> phpenmod mysql


##### Outras ferramentas

###### Git

> sudo apt-get install git

###### NodeJs

> sudo apt-get install nodejs

No vídeo, o Vedovelli faz uma coisa interessante, cria um link simbólico para **node**.

> sudo ln -s /usr/bin/nodejs /user/bin/node

Desta forma, é possível utilizar no terminal tanto **nodejs** quanto **node**.

###### npm - Gerenciador de pacotes do NodeJs

> sudo apt-get install npm

Após instalação do **npm**, vamos começar a utilizá-lo:

> npm install -g bower
>
> npm install -g gulp

###### Composer - Gerenciador de pacotes do PHP

Download do arquivo composer.phar:

> php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
>
> php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
>
> php composer-setup.php
>
> php -r "unlink('composer-setup.php');"

Após o download, colocar o composer.phar no **/usr/bin** já renomeando-o para composer.

> sudo mv composer.phar /usr/bin/composer

Desta forma, é possível utilizar globalmente **composer**.

Por enquanto é isso... outra hora continuo.

Abaixo o vídeo...

<div class="video-container">
	<iframe width="560" height="315" src="https://www.youtube.com/embed/Q2N5blJ4VIo" frameborder="0" allowfullscreen></iframe>
</div>
