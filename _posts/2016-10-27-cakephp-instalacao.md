---
layout: post
title:  "Instalação do CakePHP em servidor Nginx e PHP 7"
date: 2016-10-27 19:51:00
categories: blog
resume: Instalação do CakePHP em servidor Nginx e PHP 7.
---

## Documentação

Documentação é uma ferramenta muito importante para qualquer projeto. E eu, particularmente, gosto muito da documentação do CakePHP. Principalmente porque, sempre posso copiar e colar os exemplos, facilitando na hora de testar o código. 

## Requerimentos

> Servidor web: Apache, Nginx ou outro.

> PHP 5.5.9 ou mais recente

> Extensão intl do PHP

> Extensão mbstring do PHP

##### Instalando as extensões **intl** e **mbstring** do PHP

> sudo apt-get install php7.0-intl 

> sudo apt-get install php7.0-mbstring

## Composer

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

## Primeiro projeto CakePHP

> cd /var/www/
>
> sudo composer create-project --prefer-dist cakephp/app:3.3.* cakephp.local

Com os comandos acima, você terá a pasta **/var/www/cakephp.local** criada, mas não acessível através de uma URL. Para isso, deve configurar o Nginx criando um virtual host. 

##### Criando virtual host

> sudo subl /etc/hosts

Adicionar o endereço **http://cakephp.local** ao arquivo *hosts*.

> 127.0.1.1 cakephp.local

Criando arquivo de configuração do projeto.

> sudo subl /etc/nginx/sites-available/cakephp.local

Configuração do virtual host. 

>
> server {
>
>	listen 80;
>
>	listen [::]:80;
>
>	server_name cakephp.local;
>
>	root /var/www/cakephp.local/webroot;
>
>	index index.php;
>
>	location / {
>		try_files $uri $uri/ /index.php?$uri&$args =404;
>
>		if (-f $request_filename) {
>			break;
>		}
>
>		if (-d $request_filename) {
>			break;
>		}
>
>		rewrite ^(.+)$ /index.php?q=$1 last;
>	}
>
>	location ~ .php$ {
>		root           /var/www/cakephp.local/webroot/;
>		try_files $uri =404;
>		fastcgi_pass   unix:/run/php/php7.0-fpm.sock;
>		fastcgi_index  index.php;
>		fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
>		include        fastcgi_params;
>		fastcgi_buffer_size 128k;
>		fastcgi_buffers 256 4k;
>		fastcgi_busy_buffers_size 256k;
>		fastcgi_temp_file_write_size 256k;
>	}
>
>}
>

Ativando as configurações do projeto.

> sudo ln -s /etc/nginx/sites-available/cakephp.local /etc/nginx/sites-enabled/

Reiniciando o servidor para aplicar as alterações.

> sudo service nginx restart

Pronto!

Se aparecer a tela abaixo, é porque foi tudo feito corretamente.

![CakePHP Instalação](/images/posts/003-cakephp-instalacao.png){: .responsive-img}

