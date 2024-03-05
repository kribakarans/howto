# Setup Cgit gitweb client

1. Install Cgit and Apache webserver<br>
	`sudo apt install cgit apache2`

2. Assuming configs are auto loaded during installation. Enable below modules and restart the web-server
	```
	sudo a2enmod  cgid
	sudo a2enmod  ssl
	sudo a2enconf cgit
	sudo systemctl restart apache2
	```
3. Explore your git repositories at <http://localhost/cgit>

Take a look [here](https://raw.githubusercontent.com/kribakarans/howto/master/src/gitweb/cgitrc) for sample Cgit config file and place it in '/etc' directory.
