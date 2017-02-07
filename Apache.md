Créer un serveur virtuel
---

Lancer wamp.
Modifier c:\wamp64\bin\apache\apache2.4.23\conf\extra\httpd-vhosts.conf en ajoutant le serveur virtuel

    <VirtualHost *:80>
    	ServerName siteemploi.sf3
    	DocumentRoot C:\Users\prepavenir\Desktop\SiteEmploi\web
    	<Directory  "C:\Users\prepavenir\Desktop\SiteEmploi\web">
    		Options +Indexes +Includes +FollowSymLinks +MultiViews
    		AllowOverride All
    		Require local
    	</Directory>
    </VirtualHost>
    
Relancer les services wamp.

Ouvrir le fichier host de windows C:\Windows\System32\drivers\etc\hosts avec un editeur en mode admin<br>
Ajouter le lien entre ip et adresse du serveur virtuel

    127.0.0.1       localhost
    127.0.0.1	addressbook.sf3
    127.0.0.1	siteemploi.sf3
    
