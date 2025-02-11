Shell-Scripting

#! - Shebang notation. Used at the start to set the interpreter which will be used to execute the rest of the script.

============= Special characters =============
$?                      // Return value of last command
$0                      // Shell script name ( eg - ./shell.sh )
$1, $2, ... , $n        // nth argument to the shell script
$#                      // Number of arguments after the script name
$$                      // PID of current shell script      
$@                      // Consider input args as seperate strings
$*                      // Consider all args as single string
$!                      // Process number of last background process


============= if/elif/else ==============
if [[condition]];
then
            <statements>
elif [[condition]];
then
            <statements>
else
            <statements>
fi

============= Numeric comparisions =============
-gt, -lt, -ge, -le, -eq, -ne

============= String comparisions =============
==, !=
[[ -z "$string" ]]      // Empty string ( Either not defined or = "" )
[[ -n "$string" ]]      // Not empty string

============= Logical =============
||, &&, !

============= File ==============
[[ -e "/etc/shells" ]]              // Exists
[[ -f FILE ]]                       // File
[[ -h FILE ]]                       // Symbolic link
[[ -d FILE ]]                       // Directory
[[ -r FILE ]]                       // Readable
[[ -x FILE ]]                       // Executable
[[ -w FILE ]]                       // Writeable


============= For Loop =============
for [[condition]];
do
       <statements>
done
for i in {1..20}        // For i 1 to 20
for i in {1..20..4}     // Steps of 4 - 1,5,9,13,17
for ((i=0;i<21;i++))    // For loop like in c/c++

============= While ==============
while [[condition]];
do
            <statements>
done

============= Unitl ==============
Until the condition is not met execute.
until [[condition]]
do
            <statements>
done

============= Case =============
case "$var" in
            1) <command>;;
            2) <command>;;
            *) <command>;;
esac



============= Break/Continue ==============
Break and continue statements can be used just like in C/C++


============= Functions =============
Eg -
function foo()
{
            echo "Number of args = $#"
            echo "First arg = $1"
            echo "Script name = $0"
            return 54;
}
foo 23 34
RET=$?



============= Cut =============
cut -b 3    // Display 3rd character
cut -b 2,7  // Display 2nd and 7th character. If character does not exist on a particular line then it is not displayed.
cut -b 2-7  // Display 2nd to 7th characters.
cut -b -4   // Display start to 4th characters.
cut -b 3-   // Display 3rd to end of line characters.
            // Tabs and spaces are considered as single character.

============= Head =============
head -n 4 <file_name>           // Display first 4 lines
head -c 4 <file_name>           // Display first 4 charcters
                                // EOL is considered as one character
head -q -n 6 <file1> <file2>    // Display first six lines of each file without displaying the file name


============= Tail =============
tail -n 4 <file_name>           // Display last 4 lines
tail -c 4 <file_name>           // Display last 4 charcters. EOF also considered as a character.
tail -f <file_name>             // Track new lines added to the file


============= Head/Tail =============
head -n 22 | tail -n 11         // Display lines 12 to 22


============= Word Count ==============
wc -l       // Number of lines
wc -m       // Number of characters. EOF also considered as a character.
wc -c       // Number of bytes
wc -w       // Number of words


============= Uniq =============
uniq                    // Remove "adjacent" duplicate lines
uniq -c                 // Display count and text ( eg - 2 aa )
uniq -i                 // Case insensitive
uniq -u                 // Display lines which are not repeacted adjacently
uniq -d                 // Display only repeated lines

============= Tr ( Translate ) =============
-c          // Complement of set 1
-d          // Delete
-s          // replace each sequence of a repeated character that is listed in the last specified SET, with a single occurrence of that character

// Replaces set1 with set2 - tr [options] [SET1] [SET2]
[:digit:]   // All digits
[:alpha:]   // All alphabates
[:alnum:]   // All digits + alphabates
[:upper:]   // All upper case
[:lower:]   // All lower case
[:blank:]   // All horizontal spaces
[:space:]   // All vertical spaces

Eg -
tr "[a-z]" "[A-Z]"                  // Replace upper with lower
tr "[:upper:]" "[:lower:]"          // Replace upper case with lower case
tr "ip" "kj"                        // Replace i with k and p with j
tr "ip" "k"                         // Replace i and p with k
tr "i" "kj"                         // Replace i with k
tr -d "zd"                          // Delete all z and d
tr -cd "ks"                         // Delete everything except k and s
tr -s "[:blank:]"                   // Replace multiple blank with one blank


============ echo ============
echo "$var Text `<command>`"


============== GREP ==============
-r                      // Recursively search in given directory
-i                      // Case insensitive
-n                      // Display line number
-h                      // Do not display the file name
-H                      // With file names
-e                      // Multiple patterns
-v                      // Invert search
-w                      // Work match
-E or egrep             // Extended regex
-o                      // Display only relevant output
-l                      // Display only list of finenames
-c                      // Display number of lines which contain the word
-A -B -C                // Display n lines before, after and around output line

============ REG EXP ==============
^                       // Beginning of line
$                       // End of line
\<                      // Start of word
\>                      // End of word

.                       // Single character
[abc]                   // Any one of these characters
[^abc]                  // Any character except these 

?                       // Preceding character should be repeated zero or one time
*                       // Preceding character should be repeated zero or more times
+                       // Preceding character should be repeated one or one time

{n}, {n,}, {,m} {n,m}   // Preceding character appears 

() () \1 \2             // Capture group and remember

============ SED ============
sed -n '/abc/p' <file>                         // Print all lines containing abc
sed -n '/abc/!p' <file>                        // Print all lines not containing abc
sed -n '/abc/Ip' <file>                        // Print all lines containing abc case insensitive

sed '/abc/d' <file>                            // Print lines not containing abc
sed '/abc/!d' <file>                           // Print lines containing abc

sed 's/abc/pqr/g' <file>                       // Replace all occurances of abc with pqr
sed 's/abc/pqr/5' <file>                       // Replace 5th occurance of abc with pqr in every line
sed '5 s/abc/pqr' <file>                       // Replace abc with pqr only on the 5th line

sed '2a <Text>' <file>                         // Insert line after line number 2
sed '$a <Text>' <file>                         // Insert line at the end of file
sed '2i <Text>' <file>                         // Insert line before line 2

sed -n '1,4 p' <file>                          // Print lines 1 to 4

sed -e '<patten>' -e '<patten>' <file>         // Multiple pattens

I           // Case insensitive
g           // global
e           // Execute multiple commands
i           // Put output in the same file


============ Arithmatic operations ==============
Arithmatic operations can be performed inside (( ))
(( sum = $1 + $2 ))
sum=$(($1+$2))


============= Awk ==============
awk 'BEGIN{ ORS = " / "; FS = "," } $2 > 80  { print $2, $3 $4 } END{ print "END", NR}' file.txt
awk 'BEGIN{ FS = ","} {sum += $2} END{ print sum/NR}' marks.txt // Average of second column
NR - Number of records processed so far
NF - Number of fields in current record
FS, OFS, RS, ORS - Sperators for Input and Output fields and records
