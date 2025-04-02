```shell
safa@debian:~$ su
Mot de passe : root
sudo systemctl start apache2
netstat -ltn
ip a

mv /etc/apache2/apache2.conf /etc/apache2/apache2.conf.old
cp /etc/apache2/apache2.conf.old /etc/apache2/apache2.conf
export PATH=$PATH:"/sbin"

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

#Configuration pour le serveur DNS
nano /etc/resolv.conf

nameserver 192.168.*.*
search animauxfantastique.fr

systemctl restart apache2
```
