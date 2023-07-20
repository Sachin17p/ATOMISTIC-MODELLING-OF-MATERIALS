					Author: SACHIN PATEL

1] Basic commands to copy, move, rename, and delete the files.

2] Editor to edit the files within the terminal. nano & vi

3] Ability to change the permissions of a file.

4] Figure out which program will run the script (interpreter).

5] Execute the script in any directory of choice and figure out the output files and their locations.

6] Move the output files around for your record.

7] Every process has a process id which gets incremented automatically every time a new process is run.

8] In the virtual file system called /proc, there is a directory for every process id. This directory contains
   tons of information about the process being run.
   
9] **Command to find and replace in vi editor-->:%s/__/__/g**
   Here % implies for all lines, 
   s implies substitute
   the first blank is for regex, i.e., what has to be searched for, to replace
   the second blank is for the replacement expression 
   g implies global substitution in the entire file
   Press esc to enter the command mode
   When we don't use g, then the action is carried out only once every line

10] **'awk'** language is used for processing the incoming lines of an incoming stream
    **'gawk'** language is the same as awk but with GNU 
    The format is as follows, for example, cat data.out | awk -f script.awk
    awk script has the following format ;

    
    BEGIN{
		The lines in this section are executed only once before all lines are read.
    }
    {
		The lines in this section are executed once for every line read. 
    }
    END{
		The lines in this section are executed once after all lines are read.  
    }
    

11] **Where we can use the line-by-line processing power of awk:** 

FEM and CFD outputs coming in continuously. The streams of the line can be processed using awk like for sending alerts through emails,(SMTP-Simple Mail Transfer Protocol). 	

12] **sed --> stream editor** --> goes line by line and performs some actions on those lines

13] **sed -n '/,A/p' Slotwise\ Details.csv** --> -n suppresses the lines that do not match the pattern required.
					 --> '/,A/p' implies looking for A after a comma and printing those lines.
					 --> The argument for sed in any type of file to read from.

14] **s/\(A.\*B\)/hello\1@met/g** --> The brackets '\(' and '\)' mark the beginning and the end of the pattern, which is 
				 stored in register number 1. The '\1' implies that print that registers here.
    ex. sed 's/\(..21s...\)/\1@smail.iitm.ac.in/g' r.txt --> looks for 21s in every line with 2 characters in front 
							     and 3 characters after 21s and paste @smail.iitm.ac.in
							     after that in the r.txt file.
    ex. sed 's/\(..21s...\) \(.*\)/\1@smail.iitm.ac.in:\2/g' r.txt
    This command looks for the second pattern as well and stores it in register number 2.
    ex. sed 's/\(..21s...\)/ \2 : \1@smail.iitm.ac.in/g' r.txt 
    This command replaces the second and the first register.

15] **make utility:** make was originally designed for the compilation of codes only for the files that have changed or 
		   modified.
		   compilation --> Compile refers to the act of converting programs written in a high-level programming
                   language, which is understandable and written by humans, into a low-level binary language understood
                   only by the computer.
    ex. VASP takes an entire day for compilation, so by using make, we can reduce this time.

    In short, make is used for conditional compiling.
    make clean --> removes every file that can be compiled, specifically .o and .e files in the case of C language.
    Compilation creates an object file and an executable file.

    make compiles only those codes that have changed !!
    make reads time stamps of files to decide which one to compile.
    make looks for those files which are needed for a target to compile.
    make looks for a file called 'Makefile' or 'makefile' in the current directory.'Makefile' has  higher 
    preference over 'makefile'.
    
    A target is the result of the action on a set of files.
    Target is the exe or obj file that is created when you compile a source file.

    
    
16] **Syntax of the makefile:**

    target: list of files 
	  actions on the files (indentation is a must)
	  

    target is the object or executable files 
    action is usually a compilation 
    list of files is usually the required compiler files like *.c,*.h, etc.
    cc is for c files
    CC is for C++ files

17] make is a utility and it works above bash.

18] By typing bash in the current shell we can open another shell within the current shell, i.e., simply type 'bash'
    Verify that by using ps command. The process id(PID) will be different for the shells. The newly created shell 
    is called child shell and the old shell is called parent shell.

19] Suppose I create a variable, THISMC='SACHIN' in the parent shell. When I use echo $THISMC I will get SACHIN, in 
    the parent shell. But when I use echo $THISMC in child shell, I don't get anything. To get it in the 
    child shell, I must use export THISMC='SACHIN' in the parent shell. Now when I use echo $THISMC in the child shell
    I will get SACHIN. 

20] unset THISMC will remove the content of THISMC. 'printenv' command prints all the environmental variables of 
    the shell. 

21] **PATH is an extremely strong variable in LINUX**. For example, let us create a directory called bin in home 
    directory and then create a file called ps having the content "I hate to tell u what I am running". Now when I
    type bash ps it will give the same message. Also echo $PATH will give some default path orders in which the 
    terminal searches for in order to run ps. You can modify that by using PATH=$HOME/bin:$PATH and now when we 
    type echo $PATH the first path will be $HOME/bin as we just changed the priority of looking for paths. 
    Hence now whem we run ps it will not give the PIDs of processes but it will run our created ps.
    Now in order to run the original ps we can use /usr/bin/ps or \ps. It is a good habit to check which 'command'
    before running any command.

22] There are following type of PATH variables that are important for code development in LINUX ; 
    
    1) PATH -> The sequence of directories searched for the command you executed.
    2) LD_LIBRARY_PATH -> library files that are needed by some executables. 
       files of the type *.so which are linked after compilation
       We need the library path when we are linking. ex. #include <math.h> ; gcc file.c -lm to link the math library
     
    3) INCLUDE_PATH -> list of directories that have header/prototype declaration files for code development.
       files of the type *.hpp which are header files in C or C++ codes.
       ex. #include <OpenCL.h>


23] **How to copy and paste lines in vi editor ?**
    Go to the line and press '2' and 'd' and press enter and then go where you want to paste and press p.
    How to go to the last line in vi ? -> Use :$
    Which line it is in vi ? -> Use ctrl+G
    How to delete a specific number of lines ? -> ex.after pressing esc key, 27000dd will delete 27000 lines 
    How to insert line numbers in vi ? ->:se nu
    I want to go to the 300th line -> :300

24] **How to compress files in linux ?**
    use gzip ex. gzip syslog will compress syslog tremendously from like 16 mb to 2.5 mb. 
    use gunzip to unzip the file ex. gunzip syslog.gz
    commands to compress files -> zip , gzip , xz , bzip2
 
25] **IP addresses are of two types :** IPV4 and IPV6 ; IPV4 have 4 sets of numbers separated by '.' and the numbers are 
    from 0 to 255 while IPV6 has 6 such sets separated by '.' and uses hexadecimal numbers. 
    IPV4 has 3 types:
    
    1) local machine ip address for loopback and is usually of the form : 127.0.0.1  
       ex. you can check by using 'ping 127.0.0.1' on your local machine to check the connectivity of your network. 
       ICMP (Internet Control Message Protocol) is an error-reporting protocol that network devices such as routers 
       use to generate error messages to the source IP address when network problems prevent delivery of IP packets.
       ICMP creates and sends messages to the source IP address indicating that a gateway to the internet, such as a
       router,service or host, cannot be reached for packet delivery. Any IP network device has the capability to 
       send,receive or process ICMP messages.
       ICMP tells us whether a machine is up or not.
       
       NOTE: If a machine responds to ICMP-> machine is up
             If a machine does not respond to ping then either a) machine is down or b) ICMP is off for security 
             reasons.
             IP addresses and names : ex. aqua.iitm.ac.in -> 10.24.5.234 (DNS Domain Name Servers)
             This can be checked using nslookup aqua.iitm.ac.in
    
    2) Intranet or private addresses
       Private -> cannot be reached from outside ex. workflow and aqua of iitm
       These also come in three flavours :
       a) 10.*.*.* -> 16 million possible addresses
       b) 192.168.*.* -> 65,536 possible addresses 
       c) 172.16.*.* to 172.32.*.* -> 1 million possible addresses


    3) Global or public addresses
       These can be reached from anywhere. These addresses have to be bought against some payment and is not for 
       everybody. Also, the security threat is more because it is always active.


    NOTE : The connection request from NAC goes to -> computer center -> IITM campus switch -> ISP1 -> ISP2 -> ISP3
           -> Google server. Railtel, Tata, and Reliance are the ISPs for our campus.


26] One name many ip addresses -> service at a higher level of availability and different geographical location
    ex. ping www.google.com will give 4 different ip addresses bcoz it has to provide service across the globe and 
    hence uses a number of machines. While ping www.iitm.ac.in will give only one IP address because IITM has only 
    one machine.

    One IP address and many names ->  one server which looks like many by name to act on behalf of many websites.
 
    nslookup -> asks DNS server to resolve a name to the IP address.

    There are some license servers that offer a license to run a particular software.
   

27] The way to connect to private IP addresses is through port number. The Port is like a window.
    IP ADDRESS: PORT number is the format of a requirement for any service.
    For example when we visit any multi-specialty hospital, then there are different windows for different problems
    like dental problems on some windows, ortho problems on other windows, and so on. The same is the case with ports. 
    Ex. port no. 80 is for HTTP, port no. 22 is for SSH, and so on. 
    Port nos. up to 1000 are reserved for specific purposes. Hence if you want to provide a port number for your
    program you have to use port no. above 1000.
    For example, the Abaqus software has some IP address and some registered port no. which needs to be specified 
    while installing, only then it will run.
    netstat -tulnp tells  the IP addresses currently in use
 
28] Writing a mail using telnet from campus : 
    telnet mx.iitm.ac.in 25
    help 220 mx.iitm.ac.in ESMTP Postfix
    helo gphani.iitm.ac.in
    mail from: gphani@iitm.ac.in
    rcpt to : mm21s023@smai.iitm.ac.in
    data
    subject: test mail from class on terminal
    Hi Sachin,
    This is a test mail from campus through the terminal. 
    -gphani
    . (to close the protocol)
    quit


