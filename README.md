# assignment
shell assignment
                                             Rapidcode Technology Pvt. Ltd.
Ques1 - Write a shell script that prints “Shell Scripting is Fun!” on the screen
      	echo “Shell Scripting is Fun!”

Ques2 - Modify the shell script from exercise 1 to include a variable. The variable will hold the contents 
of the message “Shell Scripting is Fun!”
	NAME=”Shell Scripting is Fun!”
	   echo $NAME

Ques3 - Store the output of the command “hostname” in a variable. Display “This script is running on _.” 
where “_” is the output of the “hostname” command.
	HOSTNAME=$(hostname)
	echo “This script is running on $HOSTNAME”

Ques4 - Write a shell script to check to see if the file “file_path” exists. If it does exist, display “file_path 
passwords are enabled.” Next, check to see if you can write to the file. If you can, display “You have 
permissions to edit “file_path.””If you cannot, display “You do NOT have permissions to edit “file_path””
	FILE=”/home/svimukthi/Assignment/sanka”
	if [ -e “$FILE” ]
	  then
	     echo “$FILE passwords are enabled”
	fi
	if [ -x “$FILE” ]
	  then
	    echo “You have permition to execute $FILE”
	  else
	    echo “You do Not have permissions to execute $FILE”
	fi


Ques5 - Write a shell script that displays “man”,”bear”,”pig”,”dog”,”cat”,and “sheep” on the screen with 
each appearing on a separate line. Try to do this in as few lines as possible.
	ANIMALS=”man bear pig dog cat sheep”
	for ANIMAL in $ANIMALS
	  do
	    echo $ANIMAL
	  done


Ques6 - write a shell script that prompts the user for a name of a file or directory and reports if it is a 
regular file, a directory, or another type of file. Also perform an ls command against the file or directory 
with the long listing option.
	echo “Enter the file path”
	read FILE
	if [ -f “$FILE” ]
	  then
	    echo “$FILE is a reguler file”	
	elif [ -d “$FILE” ]
	  then
	    echo “$FILE is a directory”
	else
	    echo “$FILE is another type of file”
	fi
	ls -l $FILE



Ques7 - Modify the previous script to that it accepts the file or directory name as an argument instead of 
prompting the user to enter it.
	FILE=$1
	if [ -f “$FILE” ]
	  then
	    echo “$FILE is a reguler file”
	elif [ -d “$FILE” ]
	  then
	    echo “$FILE is a directory”
	else
	   echo “$FILE is another type of file”
	fi
	ls -l $FILE


Ques8 - Modify the previous script to accept an unlimited number of files and directories as arguments.
FILES=$@
for FILE in $FILES
  do
    if [ -f “$FILE” ]
      then
         echo “$FILE is a reguler file”
    elif [ -d “$FILE” ]
      then
         echo “$FILE is a directory”
    else
         echo “$FILE is another type of file”
    fi
   ls -l $FILE
  done

Ques9 - Write a shell script that displays, “This script will exit with 0 exit status.” Be sure that the script 
does indeed exit with a 0 exit status.
	echo “This script will exit with 0 exit status.”
	exit 0

Ques10 - Write a shell script that accepts a file or directory name as an argument. Have the script report 
if it is reguler file, a directory, or another type of file. If it is a directory, exit with a 1 exit status. If it is 
some other type of file, exit with a 2 exit status.

FILE=$1
if [ -f $FILE ]
  then
    echo “It is reguler File”
    exit 0
elif [ -d $FILE ]
   then
     echo “It is directory”
     exit 1
 else
    echo “Another type”
    exit 2
fi


Ques11 - Write a script that executes the command “cat/etc/shadow”. If the command return a 0 exit 
status, report “command succeeded” and exit with a 0 exit status. If the command returns a non-zero 
exit status, report “Command failed” and exit with a 1 exit status.
cat /etc/shadow

if [ “$?” -eq “0” ]
  then
    echo “Command succeeded”
    exit 0
  else
    echo “Command failed”
    exit 1
fi

Ques12 - Write a shell script that consists of a function that displays the number of files in the present 
working directory. Name this function “file_count” and call it in your script. If you use variable in your 
function, remember to make it a local variable.

function file_count()
 {
   local NUMBER_OF_FILE=$(ls -l | wc -l)
    echo "$NUMBER_OF_FILE"
 }
file_count


Ques13 - Modify the script from the previous exercise. Make the “file_count” function accept a directory 
as an argument. Next, have the function display the name of the directory followed by a colon. Finally 
display the number of files to the screen on the next line. Call the function three times. First on the 
“/etc” directory, next on the “/var” directory and finally on the “/usr/bin” directory.

function file_count()
 {
   local Directory=$1
   COUNT_FILE=$(ls $Directory|wc -l)
   echo "$Directory"
   echo "$COUNT_FILE"
 }
file_count /etc
file_count /var
file_count /usr/bin


Ques14 - Write the shell script that renames all files in the current directory that end in “.jpg” to begin 
with today’s date in the following format: YYYY-MM-DD. For example, if a picture of my cat was in the 
current directory and today was October 31,2016 it would change name from “mycat.jpg” to “2016–10–
31-mycat.jpg”.

DAY=$(date +%F)
cd /home/vimukthi/Pictures
for FILE in *.png
 do
    mv $FILE ${DAY}-${FILE}
 done


Ques15 - Write the script that renames files based on the file extension. Next,It should ask the user what 
prefix to prepend to the file name(s). By default, the prefix should be the current date in YYYY-MM-DD 
format. If the user simply press enter,the current date will be used. Otherwise,whatever the user 
entered will be used as the prefix. Next,it should display the original file name and new name of the file. 
Finally,it should rename the file.

cd /home/vimukthi/Pictures
DAY=$(date +%F)s
echo "Pleace enter the file extension:"
   read EXTENSION
echo "Pleace enter the prifix:(press enter for $DAY)"
   read
for NAME in *.$EXTENSION
 do
   echo "Renaming $NAME to ${DAY}-${NAME}"
   mv $NAME ${DAY}-${NAME}
 done


Ques16 - Created the start-up script for an application start and stop.

INPUT=$1
cd /hms/installs/mongod/mongodb-linux-x86_64-2.6.0/bin
case $INPUT in
start)
       ./mongod -f ../../mongod.conf &
       echo "Mongodb server Start"
       ;;
stop)
      PID_ID=$(ps -ef | grep mongo | cut -d" " -f3 | sed '1!d')
      kill $PID_ID
if [ $? -eq '0']
      echo "Mongodb server Stop"
      ;;
*)
     echo "Error input"
     ;;
esac
