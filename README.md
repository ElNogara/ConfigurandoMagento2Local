<h1>Instalar Magento 2.4</h1>
Documentando passo a passo de como subir Magento 2.4 na sua máquina.<br>

<h2>Configurando sua máquina.</h2>

<h3>PHP 8.1</h3>
Será necessário instalar o PHP e todas as extensões necessárias para o Magento 2 funcionar corretamente...

<h3>Composer</h3>

<h3>Mysql</h3>
Magento 2 será necessário instalar o MySQL 8.x para que funcione corretamente...

<h3>Apache2</h3>
Estarei utilizando o Apache2.4 nesse passo a passo...

<h4>Local do Magento</h4>
Dentro do servidor crie a pasta onde ficara hospedada a plataforma, no meu caso será nogaramagento então dentro de /var/www/html/ estarei criando a pasta nogaramagento/public_html

```
sudo mkdir /var/www/html/nogaramagento/
sudo mkdir /var/www/html/nogaramagento/public_html
```

Para garantir que ocorra corretamente, vou alterar as permissões dessa pasta para meu usuário e também dar um 755 para alterar as permissões de acesso, execução e alteração.
```
sudo chown -R $USER:$USER /var/www/html/nogaramagento/
sudo chmod -R 755 /var/www/html/nogaramagento/
```

Finalizado a pasta que vai receber a plataforma precisamos criar um redirecionamento no nosso servidor para essa pasta.

<h4>Criando um virtual host</h4>
Para configurar uma página no servidor devemos criar os virtuais hosts, sendo assim acesse a pasta /etc/apache2/sites-available e crie o arquivo DOMINIO.com.conf (substitua DOMINIO pelo domínio que gostaria de utilizar para acessar sua loja), dentro dele insira o conteudo:

```
<VirtualHost *:80>
  ServerAdmin email@dominio.com.br
  ServerName nogaramagento.com
  ServerAlias www.nogaramagento.com
  DocumentRoot /var/www/html/nogaramagento/public_html/pub

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined

         <Directory "/var/www/html">
               AllowOverride all
         </Directory>
</VirtualHost>
```

Ative a página:

```
sudo a2ensite nogaramagento.com.conf
``` 

<h4>Redirect arquivo hosts(Apenas para configuração em servidor local)</h4>
Caso esteja subindo o magento na sua máquina local será necessário criar um redirecionamento no seu arquivo hosts para seu VirtualHost criado no seu servidor interno. Com isso, acesse o arquivo /etc/hosts e no final de tudo insira o código:

```
127.0.2.1 nogaramagento.com
```

<h2>Instalando o Magento 2.</h2>
Execute o comando abaixo para fazer download do Magento 2 através do composer.

```
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition:2.4.5 /var/www/html/nogaramagento/public_html/
```

Acesse o diretório raiz do seu Magento, no meu caso é /var/www/html/nogaramagento/public_html/ e vamos começar a configurar, então caso seu servidor não tenha Elasticsearch instalado, antes de iniciar a configuração do Magento é necessário desativarmos os módulos que utilizam o Elasticsearch:

```
php bin/magento module:disable {Magento_Elasticsearch,Magento_InventoryElasticsearch,Magento_Elasticsearch6,Magento_Elasticsearch7}
```

Agora vamos passar alguns parâmetros para o comando de instalação do Magento:

```
php bin/magento setup:install --base-url="http://nogaramagento.com/" --db-host="localhost" --db-name="nogaramagento" --db-user="root" --db-password="SENHABANCO" --admin-firstname="Nogara" --admin-lastname="Wellington" --admin-email="email@dominio.com" --admin-user="nogara" --admin-password="SENHAADMIN" --use-rewrites="1" --backend-frontname="admin" --db-prefix=mage_
```

<strong>Espero muito ter ajudado. Mas qualquer dúvida estou a disposição - <a href="https://wellingtonnogara.com/" style="color: red;">Wellington Nogara</a>.</strong>

