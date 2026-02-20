# Shell Scripting Cheat Sheet

## Quick Reference Table

| Topic | Key Syntax | Example |
|-------|-----------|---------|
| Variable | `VAR="value"` | `NAME="DevOps"` |
| Argument | `$1`, `$2` | `./script.sh arg1` |
| If | `if [ condition ]; then` | `if [ -f file ]; then` |
| For loop | `for i in list; do` | `for i in 1 2 3; do` |
| Until | `until [ condition ] do .. done` | `until [ $i -eq 5 ] do echo $i ((i++)) done` |
| Function | `name() { ... }` | `greet() { echo "Hi"; }` |
| Grep | `grep pattern file` | `grep -i "error" log.txt` |
| Awk | `awk '{print $1}' file` | `awk -F: '{print $1}' /etc/passwd` |
| Sed | `sed 's/old/new/g' file` | `sed -i 's/foo/bar/g' config.txt` |
| Case | `case variable in a);; b);; *);; esac` | `case $num in a);; b);; *);; esac` |
| Sort | `sort file` | `sort -n log.txt` |
| Tr | `tr option [set1] [set2] < file` | `tr [a-z] [A-Z] < file` |
| Wc | `wc option file` | `wc -wcl log.txt` |
| Head | `head -n file` | `head -10 log.txt` |
| Tail | `tail -n file` | `tail -10 log.txt` |

--- 

## Task 1: Basics

1. Shebang (`#!/bin/bash`) — what it does and why it matters

* This is a shebang, first line on the script. It sets your interpreter to use `/bin/bash`.
  If it is not specified than `/bin/sh` the default interpreter will be used.


2. Running a script — `chmod +x`, `./script.sh`, `bash script.sh`

* `chmod+x` - Sets the execute permission on a file/script.
* `./script.sh` - Run the script by using the interpreter defined in script.
* `bash script.sh` - Run the script by explicitly invoking bash interprete.

3. Comments — single line (`#`) and inline

* #this is comment
* echo "hi"; #this is inline comment

4. Variables — declaring, using, and quoting (`$VAR`, `"$VAR"`, `'$VAR'`)

* name="Afroz" #declaring
* echo "$name" #using
* echo '$name' #single quote prints literally (Output: $name)

5. Reading user input — `read`

* read -p "Enter Name : " name #Take name as an input and save it in variable name

6. Command-line arguments — `$0`, `$1`, `$#`, `$@`, `$?`

* `$0` - Filename # check.sh
* `$1` - 1st argument passed by user # check.sh 6
* `$#` - Total number of arguments passed # 1
* `$@` - Prints all arguments
* `$?` - Last command's exit status

---

## Task 2: Operators and Conditionals

1. String comparisons — `=`, `!=`, `-z`, `-n`
```
a="Hello"
b="Hello"

#= Check if two strings are equal
if [[ $a = $b ]];then
	echo "Check ``=`` : True"
else
	echo "Check ``=`` : False"
fi

#!= Check if two strings are not equal
if [[ $a != $b ]];then
	echo "Check ``!=`` : True"
else
	echo "Check ``!=`` : False"
fi

#-z Check if string is empty
if [[ -z $b ]];then
	echo "Check ``-z`` Empty True : $?"
else
	echo "Check ``-z`` Empty False : $?"
fi


#-n Check if string is not empty
if [[ -n $b ]];then
	echo "Check ``-n`` Not Empty : $?"
else
	echo "Check ``-n`` Empty : $?"
fi


Output :
afroz@afroz:~/practice_sh$ ./try.sh 
a=Hello	b=Hello
Check = : True
Check != : False
Check -z Empty False : 1
Check -n Not Empty : 0

```
2. Integer comparisons — `-eq`, `-ne`, `-lt`, `-gt`, `-le`, `-ge`
```
a=3
b=4

echo -e "a=$a\tb=$b"

#-eq Check equals
if [ $a -eq $b ];then
	echo "-eq $? : Equals"
else
	echo "-eq $? : Not Equals"
fi	

#-ne Check Not Equals
if [ $a -ne $b ];then
        echo "-ne $? : Not equals"
else
        echo "-ne $? : Equals"
fi

#-lt Check Less Than
if [ $a -lt $b ];then
        echo "-lt $? : Less"
else
        echo "-lt $? : Not Less"
fi

#-gt Check Greater Than
if [ $a -gt $b ];then
        echo "-gt $? : Greater"
else
        echo "-gt $? : Not greater"
fi

#-le Check Less Than OR Equal To
if [ $a -le $b ];then
        echo "-le $? : True"
else
        echo "-le $? : False"
fi

#-ge Check Greater Than Or Equal To
if [ $a -ge $b ];then
        echo "-ge $? : True"
else
        echo "-ge $? : False"
fi

OutPut:
./int.sh 
a=3	b=4
-eq 1 : Not Equals
-ne 0 : Not equals
-lt 0 : Less
-gt 1 : Not greater
-le 0 : True
-ge 1 : False

```
3. File test operators — `-f`, `-d`, `-e`, `-r`, `-w`, `-x`, `-s`
```
<<usage
-f = If file exists and it is a regular file.
-d = If file exists and is a directory.
-e = If file exists and is a file/directory.
-r = If file exists and is readable.
-w = If file exists and is writable.
-x = If file exists and is executable.
-s = If file exists and has size greater than 0(Not Empty).
usage

read -p "Enter File Name : " fname

operators=("-f" "-d" "-e" "-r" "-w" "-x" "-s")
for oprt in "${operators[@]}";do
	if [ $oprt $fname ];then
		echo "$oprt $? : True"
	else
		echo "$oprt $? : False"
	fi
done

OutPut:
/ftest.sh 
Enter File Name : chech.sh
-f 0 : True
-d 1 : False
-e 0 : True
-r 0 : True
-w 0 : True
-x 0 : True
-s 0 : True

```
4. `if`, `elif`, `else` syntax
```
a=10
b=5
if [ $a -eq $b ];then
        echo "Equals"
elif [ $a -gt $b ];then
        echo "Greater"
else
        echo "Smaller"
fi

OutPut:
Greater

```
5. Logical operators — `&&`, `||`, `!`
```
a=10
b=5
(( ! a>b )) && echo "Smaller" || echo "Greater"

OutPut:
Smaller

```
6. Case statements — `case ... esac`
```
read -p "Choose from a,b,c : " num

case $num in
	a)
		echo "You chose a"
		;;
	b)
		echo "You chose b"
		;;
	c)
		echo "you chose c"
		;;
	*)
		echo "Invalid option"
		;;
esac

OutPut:
Choose from a,b,c : a
You chose a

Choose from a,b,c : d
Invalid option

```
---

## Task 3: Loops

1. `for` loop — list-based and C-style
```
fruits=("Apple" "Orange" "Banana" "Watermelon" "Mango" "Musk Melon")
echo "**List Based Loop**"
for fruit in "${fruits[@]}";do
        echo "$fruit"
done
echo -e "\n**C-style Loop**"
for(( i=0; i<=${#fruits[@]}; i++ ));do
        echo ${fruits[$i]}
done

OutPut:
./loop.sh 
**List Based Loop**
Apple
Orange
Banana
Watermelon
Mango
Musk Melon

**C-style Loop**
Apple
Orange
Banana
Watermelon
Mango
Musk Melon
```

2. `while` loop
```
i=5
while [ $i -gt 0 ]
do
        echo "$i"
        ((i--))
done

OutPut:
./while.sh 
5
4
3
2
1
```
3. `until` loop
```
i=3

until [ $i -eq 5 ]
do
	echo $i
	((i++))
done

OutPut:
./until.sh 
3
4
```
4. Loop control — `break`, `continue`
```
read -p "Enter any num between 1-20 : " n
for(( i=$n; i<=20 ; i++ ));do
        if [[ $i -le 0 || $i -gt 20 ]]; then
                echo "Breaking loop: $i not between 1-20" 
                break;
        fi
        if (( $i%2==0 ));then
                echo "$i = Even"
                continue;
        fi
        echo "$i = Odd"
done

OutPut:
afroz@afroz:~/practice_sh$ ./br_cnt.sh 
Enter any num between 1-20 : 0
Breaking loop: 0 not between 1-20
afroz@afroz:~/practice_sh$ ./br_cnt.sh 
Enter any num between 1-20 : 16
16 = Even
17 = Odd
18 = Even
19 = Odd
20 = Even
```
5. Looping over files — `for file in *.log`
```
for file in *.sh;do
        echo "$file"
done
```
6. Looping over command output — `while read line`
```
cat create_user.sh | while read line;do
echo "$line"
done
```
---

## Task 4: Functions

1. Defining a function — `function_name() { ... }`
2. Calling a function
3. Passing arguments to functions — `$1`, `$2` inside functions
4. Return values — `return` vs `echo`
5. Local variables — `local`

```
add() {
        local name="Afroz" #local variable
        echo "I am local variable : $name"
        echo -e "Arguments $1 , $2 " # $1&$2 arguments passed to function
        echo -e "Addition : "$(( $1 + $2 )) 
        return 
}

a=2
b=3
add $a $b #function call
echo "I am local variable trying to access outside function : $name"
echo "Function return : $? "

OutPut:
./functions.sh 
I am local variable : Afroz
Arguments 2 , 3 
Addition : 5
I am local variable trying to access outside function : 
Function return : 0 
```
---

## Task 5: Text Processing Commands

1. `grep` — search patterns, `-i`, `-r`, `-c`, `-n`, `-v`, `-E`
* `-i` : Case insensitive
* `-r` : Recursive
* `-c` : Count matching lines
* `-n` : Print each line with line number
* `-v` : Inverted match (Exclude pattern) 
* `-E` : Extended regex

2. `awk` — print columns, field separator, patterns, `BEGIN/END`
* Print Columns : `awk '{print $1,$2}'`
* Field seperator : `awk -F: '{print $1,$7}'`
* Pattern : `awk '/error/ {print $0}'`
* BEGIN : `awk 'BEGIN {print "START"}{print $3}'`
* END : `awk 'END {print "DONE"}{print $3}'`

3. `sed` — substitution, delete lines, in-place edit
* substitution : `sed 's/WARNING/CRITICAL/g' file.log` (It only prints the output unless you redirect it to a file. 
    It doesn't change the actual file.)
* delete lines : `sed '2,4d' file.log`
* in-place edit : `sed -i 's/CRITICAL/WARNING/g' file.log` (Edits the file and apply the changes.)

4. `cut` — extract columns by delimiter
* `cut -d: -f1 /etc/passwd`

5. `sort` — alphabetical, numerical, reverse, unique
* alphabetical : `sort file.txt`
* numerical : `sort -n file.txt`
* reverse : `sort -r file.txt`
* unique : `sort -u file,txt`

6. `uniq` — duplicate, count
* sort sort.txt | uniq -dc

7. `tr` — translate/delete characters
* translate : `tr [a-z] [A-Z] < sort.txt`
* delete : `tr -d a < sort.txt`

8. `wc` — line/word/char count
* `wc -wcl sort.txt`

9. `head` / `tail` — first/last N lines, follow mode
* head : `head -5 sort.txt`
* tail : `tail -5 sort.txt`

---

## Task 6: Useful Patterns and One-Liners

- Find and delete files older than N days : `find . -mtime +4`
- Count lines in all `.log` files : `wc -l file.log`
- Replace a string across multiple files : `sed 's/hello/bye/g' *.txt`
- Check if a service is running : `systemctl status ssh`
- Monitor disk usage with alerts : `df -h | awk '$5>80'`
- Tail a log and filter for errors in real time : `tail -f file.log | grep -i "error"`

---

## Task 7: Error Handling and Debugging

1. Exit codes — `$?`, `exit 0`, `exit 1`
* `$?` - Exit status of last command (0/1)
* `exit 0` - Exit if success
* `exit 1` - Exit if error

2. `set -e` — exit on error
3. `set -u` — treat unset variables as error
4. `set -o pipefail` — catch errors in pipes
5. `set -x` — debug mode (trace execution)

```
#!/bin/bash

set -euo pipefail
set -x

echo "Check set -o pipefail"
cat count.txt | grep "total"
echo "After failing script running without set -o"

echo -e "\n"
echo "Undefined variable -u"
echo $a
echo "After using undefined variable script running without set -u"

echo -e "\n"
echo "Failed command -e"
mkdir ../scripts
echo "After failing command script running without using -e"

```

6. Trap — `trap 'cleanup' EXIT`
* `trap 'echo "CleanUp"' EXIT` - It means on exit CleanUp will be printed.
  You can even define a function cleanup() and write any code you want inside `ex: rm /archive/*.gz`.
  cleanup function will be executed on EXIT of a script.

---
