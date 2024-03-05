# How to do code coverage with `Gcovr` tool

## 1. Prerequisites
Install Gcovr tool with `sudo apt install gcovr`

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

## 5. Run `gcovr` command to print a tabular report on the console
```
$ gcovr 
------------------------------------------------------------------------------
                           GCC Code Coverage Report
Directory: .
------------------------------------------------------------------------------
File                                       Lines    Exec  Cover   Missing
------------------------------------------------------------------------------
hello.c                                        6       6   100%   
------------------------------------------------------------------------------
TOTAL                                          6       6   100%
------------------------------------------------------------------------------
```

## 6. Generating HTML reports
```
$ gcovr --html-details coverage.html
```
```
$ ls
total 56K
-rw-rw-r-- 1 shanmugk shanmugk  123 Dec 11 11:08 hello.c
-rw-rw-r-- 1 shanmugk shanmugk  608 Dec 11 15:35 hello.gcno
-rwxrwxr-x 1 shanmugk shanmugk  24K Dec 11 15:35 hello
-rw-rw-r-- 1 shanmugk shanmugk  120 Dec 11 15:35 hello.gcda
-rw-rw-r-- 1 shanmugk shanmugk 7.7K Dec 11 15:51 coverage.html
-rw-rw-r-- 1 shanmugk shanmugk  10K Dec 11 15:51 coverage.hello.c.html
```
## 7. Open `coverage.html` file to browse the coverage report
```
$ firefox ./coverage.html
```
