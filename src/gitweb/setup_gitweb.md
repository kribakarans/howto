# Setup Gitweb server

1. Install `git` `gitweb` and `highlight`

2. Enable apache CGI modules and restart web server
	```
	sudo a2enmod cgi
	sudo systemctl restart apache2
	```
3. Update the Gitweb configs `/etc/gitweb.conf`
	- Added Project root to scan repositories<br>
		`$projectroot = "/home/git/projects";`
	- Enable syntax highlighting<br>
		`$feature{'highlight'}{'default'} = [1];`
	- Set project root<br>
		`$projectroot = "/home/git/projects/";`
	- Set project list<br>
		`$projects_list = "/home/git/projects.list";`
	- Take a look [here](https://raw.githubusercontent.com/kribakarans/howto/master/src/gitweb/gitweb_projects.list) for project list and save it in home directory
	- Visit [here](https://git-scm.com/docs/gitweb.conf) for more config details

4. Run the below command in project source root directory to explore your repository instantly in web-browser without adding to the config files<br>
	`git instaweb --httpd=apache2 --browser=firefox --local`<br>
	If you want to run in multiple session, randomize the port number as below<br>
	`git instaweb --httpd=apache2 --browser=firefox --local --port $[ $RANDOM % 1000 + 9000 ]'`

4. Explore your git repositories at <http://localhost/gitweb>

# Troubleshooting:
- Exec permission issue:
	`chmod +x /usr/share/gitweb/gitweb.cgi`
- Apache modules issues:
	Run `a2enmod cgi` and `a2enmod perl`
- CGIT not linked properly
	`sudo ln -s /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/`
- Sometimes noted that `/usr/share/gitweb` directory is not created on reinstall
