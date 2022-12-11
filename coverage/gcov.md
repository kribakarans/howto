# How to do code coverage with `Gcov` tool

## 1. Prerequisites
GCC comes with a code coverage tool called `gcov`. Install required tools with `sudo apt install gcc lcov`.

## 2. Sample code
```
$ cat hello.c
#include <stdio.h>

void print_hello()
{
	printf("Helloworld!!!");

	return;
}

int main()
{
	print_hello();

	return 0;
}
```

## 3. Compile source with `--coverage` or `-fprofile-arcs -ftest-coverage` flags
```
$ cc -fprofile-arcs -ftest-coverage hello.c -o hello
```
The `.gcno` record file is generated after adding the GCC compile option `-ftest-coverage`, which contains information for reconstructing the base block map and assigning source line numbers to blocks during the compilation process.
```
$ ls
total 32K
-rw-rw-r-- 1 shanmugk shanmugk 123 Dec 11 11:08 hello.c
-rw-rw-r-- 1 shanmugk shanmugk 608 Dec 11 11:08 hello.gcno
-rwxrwxr-x 1 shanmugk shanmugk 24K Dec 11 11:08 hello
```
## 4. Run the user program
Run the user program to generate the `.gcda` file that contains the coverage data counts.
```
$ ./hello 
Helloworld!!!
```
```
$ ls
total 36K
-rw-rw-r-- 1 shanmugk shanmugk 123 Dec 11 11:08 hello.c
-rw-rw-r-- 1 shanmugk shanmugk 608 Dec 11 11:08 hello.gcno
-rwxrwxr-x 1 shanmugk shanmugk 24K Dec 11 11:08 hello
-rw-rw-r-- 1 shanmugk shanmugk 120 Dec 11 11:08 hello.gcda
```

## 5. Run gcov tool to generate human readable coverage report
Run `gcov hello.c` to generate the `.gcov` text file.
```
$ gcov hello.c 
File 'hello.c'
Lines executed:100.00% of 6
Creating 'hello.c.gcov'
```
```
$ ls
total 40K
-rw-rw-r-- 1 shanmugk shanmugk 123 Dec 11 11:08 hello.c
-rw-rw-r-- 1 shanmugk shanmugk 608 Dec 11 11:08 hello.gcno
-rwxrwxr-x 1 shanmugk shanmugk 24K Dec 11 11:08 hello
-rw-rw-r-- 1 shanmugk shanmugk 120 Dec 11 11:08 hello.gcda
-rw-rw-r-- 1 shanmugk shanmugk 482 Dec 11 11:09 hello.c.gcov
```
The generated `.gcov` file looks like below
```
$ cat hello.c.gcov 
        -:    0:Source:hello.c
        -:    0:Graph:hello.gcno
        -:    0:Data:hello.gcda
        -:    0:Runs:1
        -:    1:#include <stdio.h>
        -:    2:
        1:    3:void print_hello()
        -:    4:{
        1:    5:	printf("Helloworld!!!");
        -:    6:
        1:    7:	return;
        -:    8:}
        -:    9:
        1:   10:int main()
        -:   11:{
        1:   12:	print_hello();
        -:   13:
        1:   14:	return 0;
        -:   15:}
```
The `.gcov` file contains `:` separated fields along with program source code<br>
in the format of `<execution_count>:<line_number>:<source line text>`.
 1. A count of the number of times the given line was executed<br>
	A `-` indicates a line with no executable code (e.g. a declaration)<br>
	A `#####` for lines which were never executed
 2. The line number
 3. The source code

## 6. Generating HTML reports
 ### 1. Generate the coverage.info data file
```
$ lcov --capture --directory . --output-file coverage.info
Capturing coverage data from .
Found gcov version: 9.4.0
Using intermediate gcov format
Scanning . for .gcda files ...
Found 1 data files in .
Processing hello.gcda
Finished .info-file creation
```
 ### 2. Generate a report from this data file
```
$ genhtml coverage.info --output-directory __html
Reading data file coverage.info
Found 1 entries.
Found common filename prefix "/home/shanmugk/Dropbox/frameworks/gcov"
Writing .css and .png files.
Generating output.
Processing file hello/hello.c
Writing directory view page.
Overall coverage rate:
  lines......: 100.0% (6 of 6 lines)
  functions..: 100.0% (2 of 2 functions)
```
```
$ ls __html/
total 52K
-rw-rw-r-- 1 shanmugk shanmugk  117 Dec 11 11:22 updown.png
-rw-rw-r-- 1 shanmugk shanmugk  141 Dec 11 11:22 snow.png
-rw-rw-r-- 1 shanmugk shanmugk  141 Dec 11 11:22 ruby.png
-rw-rw-r-- 1 shanmugk shanmugk  167 Dec 11 11:22 glass.png
-rw-rw-r-- 1 shanmugk shanmugk 9.7K Dec 11 11:22 gcov.css
-rw-rw-r-- 1 shanmugk shanmugk  141 Dec 11 11:22 emerald.png
-rw-rw-r-- 1 shanmugk shanmugk  141 Dec 11 11:22 amber.png
-rw-rw-r-- 1 shanmugk shanmugk 3.6K Dec 11 11:22 index-sort-l.html
-rw-rw-r-- 1 shanmugk shanmugk 3.6K Dec 11 11:22 index-sort-f.html
-rw-rw-r-- 1 shanmugk shanmugk 3.6K Dec 11 11:22 index.html
drwxrwxr-x 2 shanmugk shanmugk 4.0K Dec 11 11:22 hello
```
 ### 3. Open `index.html` file to browse the coverage report
```
$ firefox __html/index.html 
```
