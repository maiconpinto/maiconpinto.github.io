---
layout: post
title:  "Meu Ambiente de desenvolvimento!"
date:   2016-10-14 22:07:00 -0300
categories: blog
resume: 
---

## Meu Ambiente de Desenvolvimento

Recentemente tive que formatar meu notebook, e acabei procurando por um tutorial fácil e simples para configurar meu ambiente de desenvolvimento, de novo. 
Pesquisando, encontrei o vídeo abaixo, que é um dos caras feras na web, o Vedovelli.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Q2N5blJ4VIo" frameborder="0" allowfullscreen></iframe>

Abaixo segue a lista de comandos que foram utilizados no tutorial: 

- sudo apt-get update
- sudo apt-get install nginx
- sudo apt-get install mysql-server
- mysql_secure_installation
- sudo apt-get install libmcrypt4
- sudo apt-get install php7.0
- sudo apt-get install php7.0-mysql
- sudo apt-get install php7.0-mcrypt


Download Sublime Text 3 https://www.sublimetext.com/3

- sudo dpkg -i sublime-text_build-3126_amd64.deb

Configurar php.ini

```php
// /etc/php/7.0/fpm/php.ini

// trocar 
;cgi.fix_pathinfo=1

//por 
cgi.fix_pathinfo=0
```

Configurar servidor nginx `/etc/nginx/sites-available/default`.

- sudo apt-get install git
- sudo apt-get install nodejs
- sudo apt-get install npm

... por enquanto é isso, outra continuo!
