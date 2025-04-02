# Configuration du server WEB

```shell
#Partie 1 : Démarrage de Apache
safa@debian:~$ su
Mot de passe : root

sudo systemctl start apache2
netstat -ltn
ip a

mv /etc/apache2/apache2.conf /etc/apache2/apache2.conf.old
cp /etc/apache2/apache2.conf.old /etc/apache2/apache2.conf
export PATH=$PATH:"/sbin"

#Partie 2 : Configuration de Apache + Site Web
mv SAE-Site-Web-main /var/www
nano /etc/hosts
127.0.1.2 www.animauxfantastique.fr


nano /etc/apache2/sites-available/animauxfantastique.conf

<VirtualHost *:80 >
	DocumentRoot /var/www/SAE-Site-Web-main/SAE/pages/pagePrincipale
	ServerName www.animauxfantastique.fr
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


cd /etc/apache2/sites-available
a2ensite animauxfantastique.conf
#Si la commande "a2ensite" ne marche pas
/sbin/a2ensite animauxfantastiques.conf

sudo systemctl reload apache2
#sudo systemctl reload animauxfantastiques.conf

#test en cas de panne
named-checkconf animauxfantastiques.conf
sudo apchectl configtest
sudo systemctl status apache2


#Partie 3 : Configuration pour le serveur DNS
nano /etc/resolv.conf

nameserver 192.168.*.*
search animauxfantastique.fr

systemctl restart apache2

#Partie 4 : Configuration authenfication + mot de passe
cd /etc/apache2

sudo htpasswd -c .htpasswd abou
New password : abou 
Re-type new password : abou

sudo htpasswd .htpasswd gwenn
New password : gwenn 
Re-type new password : gwenn

nano /etc/apache2/apache2.conf
#Authenfication + Mot de Passe
<Directory "/var/www/SAE-Site-Web-main/SAE/pages/pagePrincipale/index.html">
	AuthType basic
	AuthName "Entrez vos indentifiants de connexion"
	AuthUserFile /etc/apache2/.htpasswd
	Require valid-user
</Directory>


systemctl restart apache2

```
# Images
## Terminal
![image](https://github.com/user-attachments/assets/dddd554b-6190-4494-abf5-99f01c84cfa0)
![image](https://github.com/user-attachments/assets/75bbb67b-505c-46ba-aee2-6533c223f56b)
![image](https://github.com/user-attachments/assets/74ba7d4f-c476-429f-8757-b58fdef63103)
## Site Web
![image](https://github.com/user-attachments/assets/9c200bb7-0fb8-4f0f-bd70-5819c6e052d1)


