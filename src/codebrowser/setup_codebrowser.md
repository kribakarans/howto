
# Setup KDAB/Woboq Codebrowser

# Build and Install Codebrowser from source
1. Install dependencies (tested in Ubuntu 20)<br>
	`sudo apt install cmake llvm clang libclang-dev`

2. Clone source code<br>
	`git clone https://github.com/KDAB/codebrowser.git`

3. Compile source with Cmake<br>
	`cmake . && make`

4. Install the binaries<br>
	`sudo make install`

# Install Codebrowser with Debian binaries
### Pre-requisites
1. Install [Bear](https://github.com/rizsotto/Bear) tool to generate 'compile_commands.json' compilation database
	- `sudo apt install bear`

2. Download and Install Codebrowser package for your system
	- Ubuntu package might requires llvm-4.0 library `sudo apt install llvm-4.0 libtinfo5`
	- Download packages for [Debian](https://download.opensuse.org/repositories/home:/pansenmann:/woboq/Debian_9.0/amd64/woboq-codebrowser_2.1_amd64.deb) and [Ubuntu](https://download.opensuse.org/repositories/home:/pansenmann:/woboq/xUbuntu_17.04/amd64/woboq-codebrowser_2.1_amd64.deb)

3. This will install couple of binaries in the system
	- `codebrowser_generator` - Generate HTML version of the source code
	- `codebrowser_indexgenerator` - Generate HTML index files

# Setup with bear tool and compile_commands.json (recommended)
1. Generate `compile_commands.json` with bear tool
	- Goto the project root directory and do `bear make` (or) `bear -- <your-build-command>`.<br>
	The output file called `compile_commands.json` is saved in the current directory.

2. Create HTML version of your source code
	- `codebrowser_generator -a -b ./compile_commands.json -p <project-name>:<project-path> -o ./output`

3. Generate HTML index files
	- `codebrowser_indexgenerator -p <project-name>:<project-path> ./output`

3. Get [Data](https://github.com/KDAB/codebrowser/tree/master/data) directory and place it in parent directory of `./output`

4. Start the web-server `python -m http.server 8000`

5. Explore the source code at <http://localhost:8000>

# Setup without bear tool
This setup doesn't require `compile_commands.json` file.

1. Create HTML version of your source code
	- `codebrowser_generator -o ./output -p <project-name>:$PWD $PWD --`

2. Generate HTML index files
	- `codebrowser_indexgenerator -p <project>:$PWD ./output`

4. Follow the steps 3 to 5 mentioned in the above section and explore code in the web-browser

# Export to webserver
1. Export the output directory `output` to your webserver
	- `sudo cp -rf ./output /var/www/html/`

6. Copy the HTML assets `data` to the parent directory
	- `sudo cp  /usr/share/woboq/data/ /var/www/html`

7. Explore your project in browser at <http://localhost/output>

# Example
`codebrowser_generator -o ./devcode -p MyProject:$PWD $PWD --`<br>
`codebrowser_indexgenerator -p MyProject:$PWD ./devcode`

# Reference
<https://woboq.com/codebrowser.html><br>
<https://github.com/KDAB/codebrowser>
