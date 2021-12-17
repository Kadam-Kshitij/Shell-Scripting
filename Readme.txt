Shell-Scripting

============= Special characters =============
$?                      // Return value of last command
$0                      // Shell script name ( eg - ./shell.sh )
$1, $2, ... , $n        // nth argument to the shell script
$#                      // Number of arguments
$$                      // PID of current shell script      
$@                      // Consider input args as seperate strings
$*                      // Consider all args as single string

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


============= For Loop =============
for <>;
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
until [[condition]]
do
            <statements>
done


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
tail -c 4 <file_name>           // Display last 4 charcters
tail -f <file_name>             // Track new lines added to the file


============= Head/Tail =============
head -n 22 | tail -n 11         // Display lines 12 to 22



============= Uniq =============
uniq                    // Remove "adjacent" duplicate lines
uniq -c                 // Display count and text ( eg - 2 aa )
uniq -i                 // Case insensitive
uniq -u                 // Display lines which are not repeacted adjacently
uniq -d                 // Display only repeated lines
