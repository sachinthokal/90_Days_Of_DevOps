# Shell Scripting Cheat Sheet

## Quick Reference Table

  Topic      Key Syntax                 Example
  ---------- -------------------------- -----------------------------------
  Variable   VAR="value"                NAME="DevOps"
  Argument   \$1, \$2                   ./script.sh arg1
  If         if \[ condition \]; then   if \[ -f file \]; then
  For loop   for i in list; do          for i in 1 2 3; do
  Function   name() { ... }             greet() { echo "Hi"; }
  Grep       grep pattern file          grep -i "error" log.txt
  Awk        awk '{print \$1}' file     awk -F: '{print \$1}' /etc/passwd
  Sed        sed 's/old/new/g' file     sed -i 's/foo/bar/g' config.txt

------------------------------------------------------------------------

# 1. Basics

## Shebang

``` bash
#!/bin/bash
```

Defines interpreter used to run script.

## Run Script

``` bash
chmod +x script.sh
./script.sh
bash script.sh
```

## Comments

``` bash
# Single line
echo "Hello"  # Inline comment
```

## Variables

``` bash
VAR="Hello"
echo $VAR
echo "$VAR"
echo '$VAR'
```

## Read Input

``` bash
read name
echo "Hi $name"
```

## Arguments

``` bash
$0  # script name
$1  # first argument
$#  # number of arguments
$@  # all arguments
$?  # last command exit status
```

------------------------------------------------------------------------

# 2. Operators & Conditionals

## String

``` bash
[ "$a" = "$b" ]
[ -z "$a" ]
[ -n "$a" ]
```

## Integer

``` bash
[ $a -eq 5 ]
[ $a -gt 3 ]
```

## File Tests

``` bash
-f file
-d dir
-r file
-w file
-x file
```

## If Statement

``` bash
if [ condition ]; then
  echo "True"
elif [ condition ]; then
  echo "Else If"
else
  echo "False"
fi
```

## Logical

``` bash
[ cond1 ] && echo "Yes"
[ cond1 ] || echo "No"
! [ cond ]
```

## Case

``` bash
case $var in
  start) echo "Start";;
  stop) echo "Stop";;
  *) echo "Invalid";;
esac
```

------------------------------------------------------------------------

# 3. Loops

## For

``` bash
for i in 1 2 3; do
  echo $i
done
```

## C-style

``` bash
for ((i=0; i<5; i++)); do
  echo $i
done
```

## While

``` bash
while [ $i -lt 5 ]; do
  ((i++))
done
```

## Until

``` bash
until [ $i -gt 5 ]; do
  ((i++))
done
```

## Break & Continue

``` bash
break
continue
```

## Files

``` bash
for file in *.log; do
  echo $file
done
```

## Command Output

``` bash
cat file.txt | while read line; do
  echo $line
done
```

------------------------------------------------------------------------

# 4. Functions

## Define & Call

``` bash
greet() {
  echo "Hello"
}
greet
```

## Arguments

``` bash
add() {
  echo $(($1 + $2))
}
add 2 3
```

## Return

``` bash
return 1
echo "value"
```

## Local

``` bash
func() {
  local var="test"
}
```

------------------------------------------------------------------------

# 5. Text Processing

## Grep

``` bash
grep -i "error" file
grep -r "text" .
grep -c "word" file
```

## Awk

``` bash
awk '{print $1}' file
awk -F: '{print $1}' /etc/passwd
```

## Sed

``` bash
sed 's/old/new/g' file
sed -i 's/foo/bar/g' file
```

## Cut

``` bash
cut -d',' -f1 file.csv
```

## Sort

``` bash
sort file
sort -n file
sort -r file
sort -u file
```

## Uniq

``` bash
uniq file
uniq -c file
```

## Tr

``` bash
tr 'a-z' 'A-Z'
```

## Wc

``` bash
wc -l file
wc -w file
```

## Head/Tail

``` bash
head -n 10 file
tail -n 10 file
tail -f log.txt
```

------------------------------------------------------------------------

# 6. Useful One-Liners

``` bash
find /path -type f -mtime +7 -delete
wc -l *.log
sed -i 's/old/new/g' *.txt
systemctl is-active nginx
df -h | grep -v tmpfs
tail -f app.log | grep "ERROR"
```

------------------------------------------------------------------------

# 7. Error Handling & Debugging

## Exit Codes

``` bash
echo $?
exit 0
exit 1
```

## Strict Mode

``` bash
set -e
set -u
set -o pipefail
set -x
```

## Trap

``` bash
trap 'echo Cleanup' EXIT
```
