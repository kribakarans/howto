# Install Redmine on Ubuntu with SQLite3

Install Redmine 5.0.5 with Apache2 and local SQLite2 database in Ubuntu Focal.

### Installing dependencies
```
apt install -y --no-install-recommends apache2 build-essential libapache2-mod-passenger libsqlite3-dev ruby-dev
```
### Download & Extract Redmine
Download the latest version from [here](https://www.redmine.org/projects/redmine/wiki/Download).  
Extract the binaries to `/opt/redmine` as below
```
mkdir /opt/redmine
tar -xf redmine-5.0.5.tar.gz -C /opt/redmine  --strip=1
```
### Configure database
Create the database configuration `/opt/redmine/config/database.yml` with below contents
```
production:
  adapter: sqlite3
  database: db/redmine.sqlite3
```
### Install and setup Ruby scripts
Run the below commands in `/opt/redmine` path to setup Ruby
```
cd /opt/redmine

gem install bundler

bundle config set --local without 'development test' 

bundle install

bundle exec rake generate_secret_token

RAILS_ENV=production bundle exec rake db:migrate

RAILS_ENV=production REDMINE_LANG=en bundle exec rake redmine:load_default_data
```
### Configure Apache
Add the config `PassengerDefaultUser www-data` in the file `/etc/apache2/mods-available/passenger.conf`.  
Now the file looks as below
```
<IfModule mod_passenger.c>
  PassengerDefaultUser www-data
  PassengerRoot /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini
  PassengerDefaultRuby /usr/bin/ruby
</IfModule>
```
Add the below contents in `/etc/apache2/sites-available/000-default.conf`
```
<Directory /var/www/html/redmine>
    RailsBaseURI /redmine
    PassengerResolveSymlinksInDocumentRoot on
</Directory>
```
Copy the HTML resources to `/var/www/html/redmine`
```
ln -sf /opt/redmine/public /var/www/html/redmine
```
Update the ownership to `www-data`
```
chown -R www-data:www-data /opt/redmine /var/www/html/redmine
```
Restart the webserver
```
service apache2 restart
```

### Access the Redmine from the local host
Explore the Redmine at <http://localhost/redmine>

### Weblinks:
[Email setup](https://www.redmine.org/projects/redmine/wiki/howto_install_redmine_on_ubuntu_step_by_step#Email-setup)  
[Backing up Redmine Database](https://www.redmine.org/projects/redmine/wiki/howto_install_redmine_on_ubuntu_step_by_step#Backing-up-Redmine)  
<https://www.redmine.org/projects/redmine/wiki/RedmineInstall>
<https://www.redmine.org/projects/redmine/wiki/howto_install_redmine_on_ubuntu_step_by_step>
<https://www.redmine.org/projects/redmine/wiki/HowTo_Install_Redmine_50x_on_Ubuntu_2004_with_Apache2>
