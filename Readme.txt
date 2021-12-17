Shell-Scripting


Cut ---->
cut -b 3    // Display 3rd character
cut -b 2,7  // Display 2nd and 7th character. If character does not exist on a particular line then it is not displayed.
cut -b 2-7  // Display 2nd to 7th characters.
cut -b -4   // Display start to 4th characters.
cut -b 3-   // Display 3rd to end of line characters.
            // Tabs and spaces are considered as single character.

Head --->
head -n 4 <file_name>           // Display first 4 lines
head -c 4 <file_name>           // Display first 4 charcters
                                // EOL is considered as one character
head -q -n 6 <file1> <file2>    // Display first six lines of each file without displaying the file name


