
# CC41 USER MANUAL 

## Version 0.45.04 Alpha

Copyright (C) 2024 Craig Bladow.  All rights reserved.

## Table of Contents
[1. Introduction](#introduction)

[2. Installation](#installation)

[3. Starting and Exiting CC41](#starting-and-exiting-cc41)

[4. Differences from HP 41CX commands](#differences-from-hp-41cx-commands)

[4. Numeric Functions](#nummeric-functions)

[5. Alpha Register](#alpha-register)

[6. Stack, Data and Alpha Register Functions](#stack,-data-and-alpha-register-functions)

[7. Display and Information Functions](#display-and-information-functions)

[8. Interactive Functions](#interactive-functions)

[9. Program and Flag Operations](#program-and-flag-operations)

[10. Extended Memory (File) Operations](#extended-memory-(file)-operations)

[11. Flags](#flags)

[12. Error Numbers](#Error-Number-Table)

## Introduction
### Why CC41?
CC41 is a re-creation of many of the functions of Hewlett Packard's HP-41CX calculator in software.  Most calculator programs recreate a graphical interface resembling a calculator requiring the user to either use a mouse to enter commands and numbers or use a somewhat non-intuitive keyboard mapping where one key on the PC's keyboard maps to a key on the graphical calculator. With CC41 you can quickly type a function such as "1/x" rather than having to memorize which keyboard key the function is mapped to.
CC41 contains 1000 data memory registers, numbered 0 to 999, and 65535 program memory registers as well as 64 flags, numbered 0 to 63. Using PATH to navigate your computer’s filesystem CC41 can read programs using GETP and GETSUB and remove them with PCLPS. CC41 can automatically load a program on launch and optionally begin running it.  
The VIEW and AVIEW commands can output results to the command window as the program runs and the TRACE and SST commands enable program debugging.
While CC41 can be a touch typist’s calculator the two best features are that programs can be written in your favorite text editor which then run incredibly fast on your computer compared to the original HP-41CX. 
### Additional Reference Material
The Hewlett-Packard HP-41 CX Owner's Manual, volumes 1 and 2, is the recommended reference for most of the commands supported by CC41.  Differences, if any, between the HP-41CX commands and CC41 will be explained in this manual.
## Installation
There is no installer needed for CC41. Download the executable corresponding to your computer's operating system and then copy the program from your download location to where you desire to run the program from. 
## Starting and Exiting CC41
Pressing the CTRL and C keys simultaneously will exit an interactive CC41 session or, if a program is running, stop the running program.  The program can be resumed by entering the RUN command.
## Enabling and Disabling Continuous Memory
To enable continuous memory, which preserves the memory and state of the calculator between uses, clear flag 59 by issuing the command, "cf 59".  This creates or updates the file "cc41.mem" upon exiting CC41. If this file is present on startup, CC41 will prompt the user to choose to restore, keep without restoring, or delete the previous saved session's state. Note that if the default path has been modified from the default, cc41.mem will be written to the modified path and won't be found automatically.  A cc41.mem file can be loaded anytime using READA.
### Windows
Open a console by pressing the Windows key located to the left of the spacebar and typing (without quotes)  "cmd".
To leave CC41 type "exit" or "off" and press the return key.
### Mac OS
Open the Terminal application by pressing the 'command' and 'space' keys to open Spotlight search, type 'terminal' and hit return.
To leave CC41 type "exit" or "off" and press the return key or press the key combination CTRL + d .
### Linux
In many linux distributions the key combination CRTL + ALT + T will open the terminal. Otherwise use the graphical menu system.
To leave CC41 type "exit" or "off" and press the return key or press the key combination CTRL + d 
### After Opening a Console Window
Navigate to the location where you copied CC41.  In Windows type "cc41" and press the return key.  

In MacOS and Linux type "./cc41" and press the return key. CC41 starts by displaying version information and some tips to get started.  This is followed by a "Memory Cleared" message and a display of the current stack values, last x value, and the contents of the alpha register.

To see the list of supported commands, enter "cat 3" and press the return key.

Commands are entered in upper or lower case with a space between each comand and number or followed by pressing the return key.

Interactive mode is where you imput commands from the keyboard, press the return key and CC41 outputs the resultant stack and alpha registers.  When you type RUN and press the return key, CC41 will begin executing the current program, at the current program step.  If you type XEQ followed by a program label, CC41 will begin running that program at the program label location. You can also GTO a program label before typing RUN.

Input is limited to 256 characters at a time. This limit includes commands, number, operations, alpha strings, and filenames. Input continues on the next entry line.  Commands that always expect a following parameter, such as SF, can be continued after the return key is pressed.  Commands that have optional following parameters, such as CLP and LIST, must be completed before pressing the return key. 

Numbers must also be completed before pressing the return key.
Numbers can be entered using keyboard keys for '+','-','.','0-9','e', and 'E'.
If more than 16 number digits are entered the the 16th digit will be rounded.

Text surrounded by double quotes, such as "Alphabet" will be placed in the Alpha Register.  Text following a command that expects text does need to be quoted. For example, GTO MYLABEL does not need double quotes.

### Command Line Options
The default mode of operation is interactive mode if no options are provided.
| Option |  Description  |
| ------ | ------------- |
| -i or -I | Start CC41 in interactive mode.
| -l or -L [filename] | Load a program into memory.
| -x or -X [filename] | Load a program into memory and begin running it.
| -r or -R [filename] | Restore entire memory from a file, equivalent to READA command.

### Command Line History
A very nice feature available is the ability to press the up and down arrows to navigate through previous commands issued to CC41.  In the Windows version of CC41 this feature works with no additional software installation needed.  For Linux and MacOS a utility called “rlwrap” needs to be installed. Once the the utility is installed then launch cc41 as follows: rlwrap ./cc41 .

## Differences from HP 41CX commands
### CC41 Additonal Commands
| CC41  |  Description  |
| ----- | ------------- |
| astol | Extended version of ASTO that stores 8 characters from the Alpha register in a memory instead of 6.
| arcl  | Extended version of ARCL that recalls 8 characters from a memory to the Alpha register instead of 6.
| ashfl | Extended version of ASHF that shifts 8 characters instead of 6 in the Alpha register.
| changes | Displays list of CC41 software changes.
| clerr | Set the error number to 0 indicating no error (see ERRNO).
| clall | Clears all memories and resets CC41 to the initial state. Not programmable.
| dec   | Input greater than 7,777,777,777,777,777 returns DATA ERROR. 
| drop  | Deletes current X contents and moves stack contents down. L not affected.
| dropl | Deletes current L contents and moves stack down. X contents moved to L.
| errno | Recalls the last error number to the X register. See [Error Numbers.](#Error-Number-Table)
| exit  | Exits CC41, similar to turning the HP-41CX off, however memory contents and status are not retained.
| exeq | Executes the system command, shell script, or batch file named in the alpha register using the current specified path.
| fview | Displays the flags register as a hexadecimal number.
| getpr | Loads and then runs a program starting at the first line.  See GETP.
| gto. |Go to the following program line number. Replaces 'GTO .'
| gto.. | Go to the end of Program Memory, create an END if the last program does not have one. Replaces 'GTO ..'
| oct   | Input greater than 281,474,976,710,655 returns DATA ERROR.
| path  | Sets the filesytem path to the contents of the alpha register.
| path? | Displays the current filesystem path, if set.
| path+ | Appends the contents of the alpha register to the current path. Maximum path characters limited to 233.
| pdir | Lists contents of the directory that PATH points to.  Defaults to the current directory.
| reada |Read calculator status, program and memory contents from PATH + filename In a program ,filename length is limited to 8 characters. 
| reads filename| Reads calculator status, written by WRTS, from PATH + filename.
| rclst | Recall stack registers X,Y,Z,T, and L from the given memory location and 4 subsequent memories.
| run   | Begins running the current program at the current step. Clears the last error (see ERRNO).
| stost | Store stack registers X,Y,Z,T, and L in the given memory location and 4 subsequent memories.
| trace | Display program step information as a program runs.
| usage | Prints how to call the CC41 executable.|
| user | Toggles flag 27 which enables USER Mode.
| wrta  | Write calculator status, program and memory contents to PATH + filename. In a program filename length is limited to 8 characters. 
| wrts filename| Write calculator status to PATH + filename. In a program filename length is limited to 8 characters. Saves registers, x, y, z, t, and l. Saves flags 0-63 and the Alpha register. Saves Statistics registers base register and data memory size allocation. 
| xail | Executes one or more commands contained in the Alpha register in line. All instructions in the Alpha register are executed. Branching due to a conditional in the Alpha register is delayed until xail completes. If any single conditional fails then the instruction following XAIL is skipped. The following commands are not allowed to be executed by XAIL: LBL, GTO, XEQ, EXEQ, RTN, STOP, PSE, PROMPT, END, XAIL and non-programmable commands. If an error is detected in the string of commands execution of the commands in the alpha register ceases.  If a program is running, the program is stopped unless flag 25 is set.
| xtoa | Doesn't replicate the special characters displayed for some codes on HP-41CX.

### Different Command Behavior
All memory, registers 0 through 999, may be directly referenced by STO, RCL, and other commands. Indirect access works also.

SIZE and PSIZE have no affect as data memory size is fixed to 1000.

SIZE? always returns 1000.

User Flags number 0-63.

Stack indirection, STO IND ST X and STO IND X will both work exactly the same.  CC41 will list commands referencing stack registers without ‘ST’.

There is no need for ALPHA or PRGM mode with CC41.  Alpha text is entered directly between double quotes and programs are edited in your favorite text editor.

The functions of the R/S key are replaced by the commands RUN and STOP.

There are no key assignments in CC41.

PRSTK prints x, y, z, and t registers as well as the l and Alpha register.

Beep prints "BEEP!" which can be suppressed by clearing flag 26.

RCLFLAG recalls status of flags 0-63 to x regiater.

STOFLAG Saves flag data in x register to flags 0-63. Viewing flag data is indicated by "Flag Data" in the display.

Numeric operations on flag data result in a "FLAG DATA" instead of an "ALPHA DATA" error.

TIME displays current time to millisecond resolution.

FIX, SCI and ENG will accept values from 0 to 15.

CC41 uses 16 decimal digits internally however only 15 can normally be displayed using FIX, SCI and ENG.  Setting flag 60 will display all sixteen digits in the current FIX, SCI or ENG formats regardless of the last FIX, SCI or ENG setting.

CLD is present for compatibility but does not clear what has been output to the console.

CC41 will not give an OUT OF RANGE error for: mdy 10.161582 -1 date+, while the HP 41CX will. 10.151582 is a valid date per the HP 41CX manual.  

### Labels
CC41 supports global labels up to 8 characters in length while HP-41CX supports 7 characters.  Global labels are case sensitive.  Valid local alpha labels for CC41 are labels a-z and A-Z except for l,x,y,z,t and L,X,Y,Z,T. Valid numeric labels are 0 through 999.

### Comments
Comments in programs may start anywhere and are prefaced by a '@' or a ';' character.  All text on a line following a comment character will be ignored.

### Entry Using Upper and Lower Case
Command entry and command short cuts are case insensitive.  File name and paths depend on your operating system settings. Program labels are case sensitive.

### Short Cut Commands
s for SST.
b for BST.
Prefacing a global label with '.' is a shortcut for XEQ. No intervening space is required.  For example, instead of XEQ TVM, typing .TVM will execute the label. This shortcut works with both local and global labels. This shortcut works in programs as well, but is expanded by LIST or SAVEP.

### User Mode
User mode is toggled by the USER command which sets flag 27 when in user mode.  When in user mode XEQ is not required to execute a global label, just type in a valid global label and it will be treated as a built-in command.

### Text Entry
Text entered between “ and “ will overwrite the contents of the Alpha regiEster. Adding a '>', ‘+’ or ‘|-‘ before the first “ will append the text to the contents of the Alpha Register (note 3).  Program labels following LBL, GTO, XEQ, READS, and filenames following WRTS, READA, WRTA, and READA do not require quotes.
CC41 uses the more easily typed "alpha" version of the HP-41CX command set as opposed to the symbols appearing on the HP-41CX keyboard.  Some of the alpha commands contain symbols that do not commonly appear on computer keyboards.  The following is a list of those commands and the text equivalent.  Either command will be accepted in a program file. Numerous other symbols produced by online RAW file decoders will also be translated or ignored.
Notes:
1. "x<>y" is the CC41 command to swap the contents of the X and Y registers.
2. Exponentiation is denoted by the '^' character e.g., x^2, y^x, e^x, 10^x, e^x-1.
3. HP-41CX printed program listings include the append character inside the double quotes. For CC41 these characters will be placed in the Alpha register so editing of these lines is necessary.


| HP-41CX | CC41   |
| ------- | ------ |
| CLΣ     | cls  |
| ENTER↑  | enter, space or return key   |
| R↑      | rup    |
| Σ+      | s+   |
| Σ-      | s-   |
| ΣREG    | sreg |
| ΣREG?   | sreg? |
| X≠0?    | x<>0? or x!=0? |
| X≠Y?    | x<>y? or x!=y? |

### Unimplemented Commands
A number of commands do not make sense in the context of CC41 vs. a handheld calculator.  There are also commands that are planned to be implemented in the future and are described as such.

## Numeric Functions
Unless noted these commands function as described in [Additional Reference Material Numeric]
(#additional-reference-material)
Because CC41 uses 16 digit decimal math, which is more digits than the HP-41CX calculator uses, the outputs of arithmetic operations may be slightly different.

| Name  | Description                                       |
| ----- | ------------------------------------------------- |
| +     | y + x                                             | 
| -     | y - x                                             | 
| *     | y * x                                             | 
| /     | y / x                                             | 
| 1/x   | Reciprocal                                        | 
| 10^x  | Common exponential                                | 
| abs   | Absolute value                                    | 
| acos  | Arc cosine                                        | 
| asin  | Arc sine                                          | 
| atan  | Arc tangent                                       | 
| chs   | Change sign                                       | 
| cos   | Cosine                                            | 
| d-r   | Degrees to radians conversion                     | 
| dec   | Octal to decimal converstion                      | 
| e^x   | Natural exponential                               | 
| e^x-1 | Natural exponential for arguments close to zero   | 
| fact  | Factorial                                         | 
| frc   | Fractional part                                   | 
| hms   | Decimal hours to hours-minutes-seconds conversion | 
| hms+  | Hours-minutes-seconds addition                    | 
| hms-  | Hours-minutes-seconds subtraction                 | 
| hr    | Hours-minutes-seconds to decimal hours conversion | 
| int   | Integer part                                      | 
| ln    | Natural logarithm                                 | 
| ln1+x | Natural logarithm for arguments close to 1        | 
| log   | Common logarithm                                  | 
| mean  | Means of accumulated x and y values               | 
| mod   | y mod x                                           | 
| oct   | Decimal to octal conversion                       | 
| p-r   | Polar to rectangular conversion                   | 
| %     | x percent of y                                    | 
| %ch   | Percent change from y to x                        | 
| pi    | Pi                                                | 
| r-d   | Radians to degrees conversion                     | 
| r-p   | Rectangular to polar conversion                   | 
| rnd   | Round                                             | 
| sdev  | Standard deviations of accumulated x and y values | 
| sum+  | Accumulations for statistics                      | 
| sum-  | Accumulations correction                          | 
| sin   | Sine                                              | 
| sign  | Sign of x                                         | 
| sqrt  | Square root                                       | 
| tan   | Tangent                                           | 
| x^2   | Square                                            | 
| y^x   | y raised to the x power                           |


## Alpha Register

The Alpha register can hold up to 24 alpha-numeric characters.

Text surrounded by double quotes, i.e. "example" will be placed in the Alpha register, overwriting any text previously there. 
If the text in double quotes is prefixed by '|-' or '+', i.e |-"pangolin" or +”anteater” then it is appended onto the existing text, if any, in the Alpha register.
A maximum of 24 characters is allowed between double quotes in interactive mode and 16 characters are allowed between double quotes in a program.

## Stack, Data and Alpha Register Functions 

| Name  | Description                      |
| ----- | -------------------------------- |
| adate | Append date in X register to Alpha register.
| aleng | Loads x with the number of characters in the Alpha register.
| anum  | Constructs a number from the first string of number characters in the Alpha register. Sets flag 22 if a number is found. 
| arcl  | Appends 6 characters from memory to Alpha register. 
| arcll | Appends 8 characters from memory to Alpha register.  
| arot  | Rotaes alpha register contents by X, left if X is positive, right if X is negative.
| ashf  | Shift Alpha register left 6 characters.
| ashfl | Shift Alpha register left 8 characters.
| asto  | Copies the left 6 characters from the Alpha register to memory.  | 
| astol | Copies the left 6 characters from the Alpha register to memory.  |        
| atime | Append time in X register to Alpha register.
| atime24 | Append time in X register to Alpha register in 24 hour format.
| atox | The value of the left most character in the Alpha register is placed in X and the Alpha register contents are shifted left one character.  A 0 is placed in X if the Alpha register is empty.
| cla   | Clear the Alpha register.
| cld   | Clear the display. Has no effect in CC41
| clrg  | Clear all numbered memory registers 
| clrgx | Clear registers starting at bbb, through eee incrementing by ii as specified in X by bbb.eeeii.
| cls | Clear statistics registers.  
| clst  | Clear the stack registers x, y, z, and t.
| clx   | Clear the x register.
| date  | Loads number for current date into the x register.
| date+ | Adds days in x register to date in y register.
| ddays | Difference in days betweein dates in the y and x registers.
| dow  | Returns the day of the week.
| dse   | Decrement the referenced register and skip the next program instruction if the counter and the end value are equal.| enter |  By itself, will duplicate x on the stack. As a space character or pressing the return key is the same as enter, enter is normally only used in programs.  
| isg   | Increment the referenced register and skip the next program instruction if the counter is greater than the end value.
| lastx | Recall register l  to x, lifting the stack.
| posa | Finds the position of the character byte code or alpha character string in X, and returns the postion of the first character to the X register.  -1 indicates that the target was not found.
| psize | Set number of data registers from program. Has no effect in CC41 as there are 1000 memory registers numbered 0 to 999.
| rup   | rotate the stack up, bringing t into x. 
| rcl | Recall a memory value to the x register.
| rdn |  rotate the stack down, putting x into t.
| regmove | The value sss.dddnnn in X specifes copying the contents of nnn registers, starting  at register sss to registers beginning with ddd.
| regswap | The value sss.dddnnn in X specifes swapping the contents of nnn registers, starting  at register sss with registers beginning with ddd.
| sumreg | Set the base memory register for the statistics registers.
| sumreg? | Recall the base memory register value for the statistics registers to the x register.
| size | Sets the number of data memory registers.  Has no effect in CC41 as there are 1000 memory registers numbered 0 to 999.
| size? | Always returns 1000. See SIZE.
| st+ | Add the x register to the referenced memory location.
| st- | Subtract the x register from the referenced memory location.
| st* | Muliply the referenced memory location by x and store the result there.
| st/ | Divide the referenced memory location by x and store the result there.
| sto | Store x in the referenced memory location.
| time | Load the current time into the x register.
| xtoa | Appends the character represented by the value in X, or the string of alpha characters in X, to the right end of the contents of the Alpha register.
| x<> | Swap the x register with the referenced memory register.
| x<>f | Swap the first 8 flags, 0-7 with the x register.
| x<>y | Swap the x and y registers.

## Display and Information Functions
| Name  | Description                            
| ----- | ---------------------------------------|
| about | Displays information about CC41 and a short summary to get started.
| adv   | To be implemented.
| aview | View the Alpha register.
| cat   |  CAT 1 lists global lables in memory.  CAT 3 lists all CC41 commands. CAT 4 lists the files in the current directory. Cat 6 lists global labels if USER mode is enabled. CAT 9 is CAT 3 with the output commands in one column. These are the only CAT commands implemented.
| changes | Displays recent software change information.
| clk12 | 12 hour clock display.
| clk24 | 24 hour clock display.
| clkt  | Only display clock time.
| clktd | Set clock to display time and date.
| clock | View clock.
| deg | Set the angle units to degrees.
| dmy | Set Day Month Year date format.
| eng | Set the display format to engineering.
| exit| Exit CC41
| fix | Set the display format to fixed.
| grad | Set the angle units to grads.
| mdy | Set Month Day Year date format.
| prstk | Print the stack, l and Alpha register.
| rad | Set the angle units to radians
| sci | Set the display format to scientific.
| trace | Display program step information as a program runs.
| usage | Displays command line parameters for loading and running programs.
| view | View the contents of the referenced memory.


## Interactive Functions
| Name  | Description                                  
| ----- | ----------- | 
| beep  | Prints "BEEP!". Output can be suppressed by clearing flag 26.
| exit  | Exit CC41 program. Memory and status are not saved.
| off   | Exit CC41 program. Memory and status are not saved.
| prompt | Stops a running program and displays Alpha register prompt.  User enters the needed data and types RUN followed by pressing the return key.
| pse   | Pauses running program for 2 seconds. CC41 does not accept input during a pause.
| tone  | Not yet implemented.

## Program and Flag Operations

Flag test operations will print 'yes' or 'no' when commanded in interactive mode. See [11. Flags](#flags) for flag definitions.

| Name  | Description | 
| ----- | ----------- |
| bst   | Step back one program line.
| cf    | Clear flag.
| clp   | Clear program.
| end   | End of program. 
| fc?   | Test if flag is clear.
| fc?c  | Test if flag is clear. Then clear the flag.
| fs?   | Test if flag is set.
| fs?c  | Test if flag is set. Then clear the flag.
| gto   | Go to a program label.
| gto.  | Go to a program line number.
| gto.. | Go to the end of program memory and append and END statement to the last program if none is present.
| lbl   | Program label. Valid numeric labels are 0 through 999. Alpha-numeric labels can be up to 8 characters in length. Invalid labels are x, y, z, t, l, X, Y, Z, T, and L. Numeric only and single alpha labels are local in scope to the current program, all other labels are globally accessible from any program in memory.
| list  | list the program from the current step. If followed by a number N, list N program lines from the current program step.
| pclps| Programmable version of CLP.  Clears a program with the label as identified in the Alpha register.
| rclflag | Recalls status of flags 0-63 to x regiater.
| rtn   | Directs program to return to the calling program or exit.
| run   | Start running the program at the current program step.
| sst   | Execute one step of the program.
| stoflag | Saves flag data in x register to flags 0-63.
| stop  | Command in the running program to stop.
| x=0?  | Test if x is equal to 0.
| x<>0? | Test if x is not equal to 0.
| x<0?  | Test if x is less than 0.
| x<=0? | Test if x is less than or equal to 0.
| x>0?  | Test if x is greater than 0.
| x=y?  | Test if x is equal to y.
| x<>y? | Test if x is not equal to y.
| x<=y? | Test if x is less than or equal to y.
| x<y?  | Test if x is less than y.
| x>y?  | Test if x is greater than y.
| xeq   | Execute a program starting at the given program label. XEQ does not clear errors (see ERRNO).

## Progam Development Functions
These features help in devloping and debugging programs.  A list of up to 25 registers may be monitored.  The contents of the registers will be displayed everytime the statck is displayed.  Registers can be added and removed one at a time using WATCH and UNWATCH respectively. WATCH and UNWATCH take the same arguments as VIEW.
| Name  | Description                                       
| ----- | ------------ |
| clwatch | Clear the list of watch registers.
| unwatch (0 to 999, ind, st)| Unwatch the referenced storage register   
| watch (0 to 999, ind, st)| Watch the referenced storage register. 

## File Operations (Extended Memory)
Data and text file operations are not currently supported in CC41.
| Name  | Description                                       
| ----- | ------------ |
| pdir | List files in the directory pointed to by PATH.
| emdir | List files in the default directory.
| getp  | Reads a program into memory, replacing the last program in memory. Uses PATH plus the filename stored in the Alpha Register. If getsub is commanded from a running program, execution resumes after the getsub command. If the program has line numbers, every line must have a number, the line numbers do not have to be in any order and can be duplicated.  This is useful if you add comments to an existing program with line numbers. 
| getr | Copies registers from the file named in the Alpha register plus PATH into main memory.
| getrx | Copies registers from the file named in the Alpha register plus PATH into main memory starting at sss and ending at eee where sss.ee is a number in the x register.
| getsub| Reads a program into memory after all other programs. Uses PATH plus the filename stored in the Alpha Register and PATH. If getsub is commanded from a running program, execution resumes after the getsub command.
| path  | Sets the filesytem path to the contents of the alpha register. Initializes to the current directory.
| path? | Displays the current filesystem path.
| path+ | Appends the contents of the alpha register to the current path. Maximum path length is limited to 233 characters.
| reada |Read calculator status, program and memory contents from PATH + filename In a program ,filename length is limited to 8 characters.
| reads filename| Reads calculator status, written by WRTS, from PATH plus filename. 
| saver | Saves all registers in main memory to the file named in the Alpha register plus PATH
| savep | Saves a program with the designated global label to the named file. Line numbers are included and may be turned off by setting flag 58. Output of SAVEP should be compatible with RAW file converter utilities comp41 from lifutils and also 41uc.
| saverx | Copies registers to the file named in the Alpha register plus PATH from main memory starting at sss and ending at eee where sss.ee is a number in the x register.
| wrta  | Write calculator status, program and memory contents to PATH + filename. In a program filename length is limited to 8 characters. 
| wrts filename| Write calculator status to PATH + filename. In a program filename length is limited to 8 characters. Saves registers, x, y, z, t, and l. Saves flags 0-63 and the Alpha register. Saves Statistics registers base register and data memory size allocation. 

## Flags

Flags typically follow the HP-41CX conventions with flags 0-29 being user modifiable.  System flags are 30-63, where HP-41CX stops at flag 55.
Currently all flags are user modifiable, this may change in the future.

# Flag Overview
| Flag No.  | Description                                       
| --------- | ------------ |
| 0-10  | User Flags
| 11-29 | Control Flags
| 30-61 | System Flags
| 62-63 | Console Output Flags

# Control Flags
Flags identified as "Reserved" are not currently implemented but may be used in a future version of CC41. They can currently be set, cleared and tested by the user.
| Flag No.  | Description                                       
| --------- | ------------ |
| 11    | Reserved (Automatic Execution)
| 12-20 | Reserved (External Device Control)
| 21    | Reserved (Printer Enable)
| 22-23 | Reserved (Data Input)
| 24 | RangeError Ignore
| 25 | Error Ignore
| 26    | Audio Enable, when set enables output to console from BEEP command.
| 27    | User Mode enabled when set.
| 28-29 | Display Punctuation

# System Flags
Flags identified as "Reserved" are not currently implemented but may be used in a future version of CC41. They can currently be set, cleared and tested by the user.
| Flag No.  | Description                                       
| --------- | ------------ |
| 31    | Date Format page 242
| 36-39 | Number of displayed digits page 160-161
| 42-43   | Angular Mode page 186
| 44 | Reserved (Continuous On)
| 48    | Reserved (Alpha Keyboard active)
| 49    | Reserved (Low Battery)
| 50 | Reserved (Message Displayed)
| 55 | Reserved (Printer present)
| 56-57 | Reserved CC41 system Flag

# Miscellaneous CC41 System Flags
| Flag No.  | Description                                       
| --------- | ------------ |
| 58 | Setting this flag disables line numbers being output by the LIST and SAVEP commands
| 59 | When cleared enables continuous memory functionality. This flag is set on startup.

# Console Display Flags
Console display flags determine what is displayed as console output as a result of user interaction. These flags can be set, cleared and tested by the user.
| Flag No.  | Description                                       
| --------- | ------------ |
| 60 | When set will display the 16th digit in the number regardless of the current FIX, ENG and SCI setting.  This flag is clear on startup.
| 61 | When set suppresses "Reading/Writing filename.ext" messages when reading or writing files. This flag is clear on startup.
| 62 | Displays just the X register contents instead of the entire stack when set. This flag is clear on startup.
| 63 | Display stack and alpha register contents when set. This flag is set on startup. Clearing this flag results in no output. 

## Error Number Table
| Error No. | Description
| --- | ------------ |
| 0 | No Error
| 1 | Data Error
| 2 | Out of Range Error
| 3 | Nonexistent 
| 4 | Alpha Data
| 5 | Flag Data
| 6 | Memory Lost
| 7 | Xail Error
| 99 | Unknown Error





    
