# Bootcamp notes

## Linux / shell
***

Shell is a command interpreter. BASH and Zshell are its implementations.
- `ps -e` or `ps aux` for active processes;
- kill <process id> to stop a process;
- stats command:
	```bash
	 stat -f "%N - %z - %Sm - $(shasum -a 256 src/test.txt|grep -Eo '^[^ ]+') - sha256" -t "%Y-%m-%d %H:%M"  src/test.txt
	```
- and log it:
	```bash
	echo $(stat -f "%N - %z - %Sm - $(shasum -a 256 src/test.txt|grep -Eo '^[^ ]+') - sha256" -t "%Y-%m-%d %H:%M"  src/test.txt) >> my.log
	```
- replace a text string:
	```bash
	sed -i '' 's/Lorem ipsum dolor sit amet,/new text/' test.txt
	```
- my first bash script:
	```bash
	#!/bin/bash

	FILE_PATH=$1
	STRING_OLD=$2
	STRING_NEW=$3

	if [ -z "$FILE_PATH" ]
		then echo "Specify the file path"
		exit 0
	elif [ -z "$STRING_OLD" ]
		then echo "Specify the string that should be replaced"
		exit 0
	elif [ -z "$STRING_NEW" ]
		then echo "Specify the string to be replaced with"
		exit 0
	fi

	sed -i '' "s/$STRING_OLD/$STRING_NEW/" $FILE_PATH
	echo $(stat -f "%N - %z - %Sm - $(shasum -a 256 $FILE_PATH|grep -Eo '^[^ ]+') - sha256" -t "%Y-%m-%d %H:%M"  src/test.txt) >> src/files.log
	```

## Introduction to C
***
- GCC compiler comand example.
	```bash
	gcc -std=c11 -Wall -Werror -Wextra src/hello.c
	```

- new note here


## Additional
***

### Project tips
- All changes should be made in `deveolop` branch;

### Good to know
- Create a text file with some content:
	```bash
	echo "Hello, Word\!" > hello-world.txt
	```
