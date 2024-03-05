# Setup GNU Global source code tagging

This article is written based on the [GNU Global](https://www.gnu.org/software/global/globaldoc_toc.html) tutorial.<br>
Follow the below steps in the root directory of the project source code.

1. Install required tools<br>
	`apt install global cflow` #Cflow is optionally need to generate call-tree

2. Generate `Gtags`<br>
	`gtags --explain --skip-symlink --statistics`

3. Generate `Htags`<br>
	```
	htags --auto-completion --colorize-warned-line --dynamic --frame --form --fixed-guide \
	      --icon --line-number --map-file --other --symbol --show-position --table-list \
	      --warning --func-header=right --tree-view=filetree \
	      --title 'Welcome to XXXX source code navigation!'
	```
4. See the [man page](https://manpages.ubuntu.com/manpages/trusty/man1/global.1.html) for command line usage. Here we will discuss the usage of the HTML version.

5. Running `htags` will generate the static HTML pages in the `HTML` folder in the current path.<br>
   Open the web browser with HTML file as an argument and explore the source code.<br>
	`firefox HTML/index.html`

6. Alternatively to the step 5, run [Htags-server](https://manpages.ubuntu.com/manpages/bionic/man1/htags-server.1.html) and connect through the <http://localhost:8000><br>
	```
	$ htags-server
	Python2 http/cgi server
	Serving HTTP on 127.0.0.1 port 8000 ...
	```
