<h1>Instalar Magento 2.4</h1>
Documentando passo a passo de como subir Magento 2.4 na sua máquina.<br>

<h2>Configurando sua máquina.</h2>

<h3>PHP 8.1</h3>
Será necessário instalar o PHP e todas as extensões necessárias para o Magento 2 funcionar corretamente...

<h3>Mysql</h3>
Magento 2 será necessário instalar o MySQL 8.x para que funcione corretamente...

<h3>Apache2</h3>
Estarei utilizando o Apache2.4 nesse passo a passo...

<h4>Local do Magento</h4>
Dentro do servidor crie a pasta onde ficara hospedada a plataforma, no meu caso será nogaramagento então dentro de /var/www/html/ estarei criando a pasta nogaramagento/
```
sudo mkdir /var/www/html/nogaramagento/
```

Para garantir que ocorra corretamente, estarei alterando as permissões dessa pasta para meu usuário e também 755
```
sudo chown -R $USER:$USER /var/www/html/nogaramagento/
sudo chmod -R 755 /var/www/html/nogaramagento/
```

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


sudo a2ensite nogaramagento.com.conf
<strong>Espero muito ter ajudado. Mas qualquer dúvida estou a disposição - <a href="https://wellingtonnogara.com/" style="color: red;">Wellington Nogara</a>.</strong>

