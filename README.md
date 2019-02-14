# Server-Digital-Ocean

# Baixar as Atualizações Ubuntu 
sudo apt-get update

# Upgrade das Atualizações
 sudo apt-get upgrade

# Instalação do Apache
 sudo apt-get install apache2

# Teste de Erro do Apache
 sudo apache2ctl configtest

# Correção Erro e Adicionar ServerName ip_do_seu_server
 sudo nano /etc/apache2/apache2.conf

# Instalação do Mysql Server
 sudo apt-get install mysql-server

# Ativar Configurações de Segurança Mysql
 mysql_secure_installation

# Conectando ao mysql
 sudo mysql -u root -p

# Mostrar tabelas
 show databases;

# Sair do Mysql
 exit;

# Instalação do PHP com Alguns Pacotes
 sudo apt-get install php7.0 libapache2-mod-php php-mysql php-intl php-curl php-mbstring

# Dar Prioridade ao PHP no Apache
 nano /etc/apache2/mods-enabled/dir.conf

# Configurar Virtual Host para um Domínio
# Acesse a Pasta
 cd /etc/apache2/sites-available/

# depois copie o arquivo 000-default.conf
 cp 000-default.conf dominio.com.br.conf

# Configuração para Domínio Principal

#<VirtualHost *:80>
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
#</VirtualHost>

# Depois Ative a configuração do arquivo dominio.com.br.conf
 sudo a2ensite dominio.com.br.conf
 
 # Depois Copie o Arquivo dominio.com.br.conf para Gerar o Subdomínio
 cp dominio.com.br.conf subdominio.dominio.com.br.conf
 
# Configuração para Subdomínio

#<VirtualHost *:80>
        ServerAdmin contato@dominio.com.br
        ServerName  subdominio.dominio.com.br
        ServerAlias subdominio
        DocumentRoot /var/www/subdominio.dominio.com.br/public_html/

        <Directory /var/www/subdominio.dominio.com.br/public_html/ >
            Options Indexes FollowSymLinks MultiViews
            AllowOverride all
            Order allow,deny
            allow from all
        </Directory>
        
        #Logfiles
        #ErrorLog  /var/www/subdominio.dominio.com.br/logs/error.log
        #CustomLog /var/www/subdominio.dominio.com.br/logs/access.log combined
#</VirtualHost>

# Depois Ative a configuração do subdominio.dominio.com.br.conf
 sudo a2ensite subdominio.dominio.com.br.conf
 
# Reinicie o Apache2 para Carregar as Novas Alterações
sudo service apache2 restart

# Configuração do php.ini 
# Caminho /etc/php/7.0/apache/php.ini
file_uploads = On
allow_url_fopen = On
memory_limit = 256M
upload_max_filesize = 20M
max_execution_time = 360
date.timezone = America/Sao_Paulo

# Ativar Modo rewrite do Apache
 sudo a2enmod rewrite

# Adicionar Certificado SSL
# https://certbot.eff.org/lets-encrypt/ubuntutrusty-apache.html

 sudo apt-get update
 sudo apt-get install software-properties-common
 sudo add-apt-repository universe
 sudo add-apt-repository ppa:certbot/certbot
 sudo apt-get update
 sudo apt-get install certbot python-certbot-apache 

# Criar Certificado para o Domínio e Subdomínio
 certbot --apache -d dominio.com.br -d www.dominio.com.br

# Adicionar Cron de Renovação Automática, o Certificado Expira a Cada 3 meses
 certbot renew --dry-run
