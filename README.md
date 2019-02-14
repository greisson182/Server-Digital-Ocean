# Server-Digital-Ocean

# Baixar as Atualizações Ubuntu 
sudo apt-get update

# Upgrade das Atualizações
 sudo apt-get upgrade

# Instalação do Apache
 sudo apt-get install apache2

#  teste de erro do apache
 sudo apache2ctl configtest

# Correção Erro e adicionar ServerName ip_do_server
 sudo nano /etc/apache2/apache2.conf

# Instalação do Mysql Server
 sudo apt-get install mysql-server

# Ativar Configurações de Segurança Mysql
 mysql_secure_installation

# Conectando ao mysql
 sudo mysql -u root -p

# Mostrar tabelas
 show databases;

# sair
 exit;

# Instalação php
 sudo apt-get install php7.0 libapache2-mod-php php-mysql php-intl php-curl php-mbstring

# Dar Prioridade ao php no apache
 nano /etc/apache2/mods-enabled/dir.conf

# Configurar vitual host para um domínio
# Acesse a Pasta
 cd /etc/apache2/sites-available/

# depois copie o arquivo 000-default.conf
 cp 000-default.conf dominio.com.br.conf

# Depois Edite o Arquivo

<VirtualHost *:80>
        ServerAdmin contato@dominio.com.br
        ServerName  dominio.com.br
        ServerAlias www.dominio.com.br
        DocumentRoot /var/www/dominio.com.br/public_html/

        <Directory /var/www/dominio.com.br/public_html/ >
            Options Indexes FollowSymLinks MultiViews
            AllowOverride all
            Order allow,deny
            allow from all
        </Directory>
        
        #Logfiles
        #ErrorLog  /var/www/dominio.com.br/logs/error.log
        #CustomLog /var/www/dominio.com.br/logs/access.log combined
</VirtualHost>

# Depois Ative a configuração do arquivo dominio.com.br.conf
 sudo a2ensite dominio.com.br.conf

# Configuração do php.ini 
# Caminho /etc/php/7.0/apache/php.ini
file_uploads = On
allow_url_fopen = On
memory_limit = 256M
upload_max_filesize = 20M
max_execution_time = 360
date.timezone = America/Sao_Paulo

# ativar modo rewrite
 sudo a2enmod rewrite

# adicionar certificado ssl
# https://certbot.eff.org/lets-encrypt/ubuntutrusty-apache.html

 sudo apt-get update
 sudo apt-get install software-properties-common
 sudo add-apt-repository universe
 sudo add-apt-repository ppa:certbot/certbot
 sudo apt-get update
 sudo apt-get install certbot python-certbot-apache 

# criar certificado para o domínio
 certbot --apache -d dominio.com.br -d www.dominio.com.br

# adicionar cron de renovação automática
 certbot renew --dry-run