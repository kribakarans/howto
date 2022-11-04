# Setup OpenGrok

This article is written based on [OpenGrok Wiki](https://github.com/oracle/opengrok/wiki/How-to-setup-OpenGrok) and deployed in Ubuntu 20 distro.<br>
Switch to `sudo` mode and follow the below steps.

### Method 1:
Setting OpenGrok with [opengrok-1.5.12.tar.gz](https://github.com/oracle/opengrok/releases/download/1.5.12/opengrok-1.5.12.tar.gz) release.

1. Setup requires `universal-ctags` `tomcat9` `default-jre` and `python3`
	```
	sudo apt remove  -y exuberant-ctags # Remove if it exist
	sudo apt install -y universal-ctags python3-pip tomcat9 # tomcat automatically install jdk
	```
2. Add required directories<br>
	`mkdir -p /opengrok/{src,data,dist,etc,log}`

3. Copy your project sources to `/opengrok/src` directory. Each directories will be treated as projects

4. Extract downloaded Opengrok release package<br>
	`tar -C /opengrok/dist --strip-components=1 -xzf opengrok-1.5.12.tar.gz`

5. Updated logging properties. Copy below contents to `/opengrok/etc/logging.properties` file
	```
	handlers= java.util.logging.FileHandler, java.util.logging.ConsoleHandler

	java.util.logging.FileHandler.pattern = /opengrok/log/opengrok%g.%u.log
	java.util.logging.FileHandler.append = false
	java.util.logging.FileHandler.limit = 0
	java.util.logging.FileHandler.count = 30
	java.util.logging.FileHandler.level = ALL
	java.util.logging.FileHandler.formatter = org.opengrok.indexer.logger.formatter.SimpleFileLogFormatter

	java.util.logging.ConsoleHandler.level = WARNING
	java.util.logging.ConsoleHandler.formatter = org.opengrok.indexer.logger.formatter.SimpleFileLogFormatter

	org.opengrok.level = FINE
	```
6. Install OpenGrok tools to deploy and build index<br>
  `pip install /opengrok/dist/tools/opengrok-tools.tar.gz `

7. Deploy OpeGrok webapp to Tomcat servelet<br>
  `opengrok-deploy -c /opengrok/etc/configuration.xml /opengrok/dist/lib/source.war /var/lib/tomcat9/webapps`

8. Generate Index for your projects
	```
	opengrok-indexer -J=-Djava.util.logging.config.file=/opengrok/etc/logging.properties \
	           -a /opengrok/dist/lib/opengrok.jar -- \
	           -c /usr/bin/ctags-universal \
	           -s /opengrok/src \
	           -d /opengrok/data \
	           -W /opengrok/etc/configuration.xml \
	           -U http://localhost:8080/source \
	           -H -P -S -G -i '*.out' -i '*.swo' -i '*.swp' \
	           -i '*.a' -i '*.d' -i '*.o' -i '*.so' -i '*.so.*' \
	           -i d:__ktags -i d:obj -i d:dist -i d:sandbox -i d:codereview -i 'd:*-build'
	```
9. Explore the deployed projects at <http://localhost:8080/source/>

### Method 2:
Setting OpenGrok with [opengrok-1.1-rc32.tar.gz](https://github.com/oracle/opengrok/releases/download/1.1-rc32/opengrok-1.1-rc32.tar.gz) release candidate. See the transition guide [here](https://github.com/oracle/opengrok/wiki/Python-scripts-transition-guide).

1. Install required software
	```
	sudo apt install -y universal-ctags python3-pip tomcat8 # tomcat automatically install jdk
	```
2. Add required directories<br>
	`mkdir -p /opengrok/{src,data,dist,etc,log}`

3. Copy your project sources to `/opengrok/src` directory. Each directories will be treated as projects

4. Extract downloaded Opengrok release package<br>
	`tar -C /opengrok/dist --strip-components=1 -xzf opengrok-1.1-rc32.tar.gz`

5. Updated logging properties `/opengrok/etc/logging.properties` as mentioned in above method at step 5.

6. Go to the directory `/opengrok-1.1-rc30/bin/` follow next steps

7. Deploy OpenGrok with `./OpenGrok deploy` command

8. Index your projects `./OpenGrok index` command

9. Explore the deployed projects at <http://localhost:8080/source/>

