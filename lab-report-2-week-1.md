# Week 1 Lab: Remote Access

## In this tutorial you will learn how to:
1. Access a remote server using `ssh` (Secure Shell) protocol.
2. Run commands on the remote server. 
3. Use `scp` (Secure Copy) to copy files to the remote server. 
4. Optimize running code on the remote server.

<br>

---
## Step 1 - Installing VScode:
<br>

![](/vscode.png)
Screenshot of VScode open.

<br>

**Before you can begin connecting remotely, a workspace is needed:**
* Head to the VScode website: [https://code.visualstudio.com/](https://code.visualstudio.com/) and follow instuctions to download and install the program on your computer.
* Once installed, open the application and make sure the window that appears is like the image shown above.
* _Note_: Depending on settings and your operating system, your VScode window may not look exactly like the image.

<br>

---
## Step 2 - Remotely Connecting:
<br>

> If you are on a Windows machine, begin by checking that the **OpenSSH Client** is installed.
> * Go to: [OpenSSH for Windows](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui) and follow the directions under the **Install OpenSSH for Windows** section.
> * _Note_: Make sure to only install the Client and **NOT** the Server.

<br>

![](/terminalOpen.png)
* With VScode open, press **Ctrl or Command + `** or go to the **Terminal tab -> New Terminal** to open the terminal.

![](/part4.png)
A succesful connection to UCSD's ieng6 server.

<br>

* From the terminal, to remotely connect to one of UCSD's servers, in this case the **ieng6** server, you will need the username and password to your CSE course-specific account.
* In the terminal enter:<br>`ssh cs15lfa22XX@ieng6.ucsd.edu`<br>Replace the **XX** with the appropirate letters from your username.
* _Note_: If it is your first time connecting to the server you will be prompted with a message asking if you want to continue connecting. Type `yes` and press enter to proceed with the connection.
* You will then be prompted for your password to your course-specific account. Type it, then press enter.

**If you followed the steps correctly, your terminal should show text similar to what is displayed in the above image.**

* __You are now logged into the remote server!__

<br>

---
## Step 3 - Trying Some Commands:
<br>

![](/commandsRun.png)
Various commands run on both the remote server and the client computer.

<br>

* On both your computer and the remote server enter the following commands and oberve what happens:<br>-- `ls`<br>-- `pwd` (*Print Working Directory*)<br>-- `ls -lat` (*List all files in directory in a long listing format with the files sorted by modification time, newest first*)<br>-- `ls -a` (*List all files*)
* Depending on the operating system from which the commands are run, they may work or throw an error as illustrated in the above image.
* On the remote server enter the following commands and observe what happens:<br>-- `ls <directory>` (In this case, `<directory>` is `/home/linux/ieng6/cs15lfa22/cs15lfa22abc`)<br>-- `cat /home/linux/ieng6/cs15lfa22/public/hello.txt`
* After running the commands, your terminal(s) should look like the above image.
* _Note_: To open a split screen terminal like in the image, click on the split screen terminal icon: ![](/splitTerminal.png) in the terminal window in VScode.
* _Note_: To exit the remote server type `exit` into the remote terminal and press enter.

**By running commands on both the remote server and your computer, it is evident that the commands on the remote server are accessing that server's file system given the different outputs from the same commands.**

<br>

---
## Step 4 - Moving Files with `scp`:
<br>

![](/WhereAmIJava.png)
WhereAmI.java file in VScode.

<br>

To explore moving files to the remote server using `scp`, create an empty folder and open that folder in VScode using **File -> Open Folder**. Under the folder, create a new file and name it `WhereAmI.java`.

<br>

In `WhereAmI.java` copy/paste the following code into it:
```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```
*Make sure to save `WhereAmI.java`*

Your VScode window should contain something similar to the above image in it.

<br>

![](/part6.png)
Terminal(s) following execution of code on the remote server and client computer.

<br>

* To run `WhereAmI.java` on the remote server begin by running the following command on your computer to copy `WhereAmI.java` to the remote server:<br>`scp WhereAmI.java cs15lfa22XX@ieng6.ucsd.edu:~/`
* `ssh` into the remote server and run the following commands in sequence to execute the program in the remote server:<br>1. `javac WhereAmI.java`<br>2. `java WhereAmI`
* Run the same two commands on your computer terminal to execute the program on your computer.
* Your terminal(s) should be similar to the above image.

**Depending on where `WhereAmI.java` is executed, it prints the relevant operating system information from the system it was run from.**

<br>

---
## Step 5 - Setting an SSH Key:
<br>

> Setting an `ssh` key allows you to log into a particular remote server and send files to that server without having to type your password each time, saving time.

<br>

![](/part7.png)
Logging onto ieng6 with an `ssh` key. (*Notice no password is required*)

<br>

* To set up an `ssh` key for the ieng6 server begin by entering `ssh-keygen` into your computer terminal.
* When your terminal asks: `Enter file in which to save the key` press **enter** to specify the default path in which to save the key. (*Take note of the path*)
* When your terminal asks: `Enter passphrase` press **enter** to specify no passphrase.
* From there a public key: `id_rsa.pub` and private key: `id_rsa` will be created and saved to your computer in the `.ssh` directory.
* `ssh` into the remote server and enter the following command: `mkdir .ssh`. Then `exit` the remote server.
* On your computer terminal enter the following command to copy the public key to the `.ssh` directory you created on the remote server:<br>`scp /Users/<User>/.ssh/id_rsa.pub cs15lfa22XX@ieng6.ucsd.edu:~/.ssh/authorized_keys`<br>-- *Note*: On Windows the client directory is: `\Users\<User>/.ssh/id_rsa.pub`<br>-- *Note*: `<User>` is the username of your computer.

**If done correctly, you should now be able to log into the ieng6 server and copy files to it without having to enter your password. Logging onto the ieng6 server with a `ssh` key is illustrated in the above image.**

<br>

---
## Step 6 - Optimizing Remote Running:
<br>

![](/part8.png)
Commands combined in a single line to copy `WhereAmI.java` to the remote server and execute the program on the remote server.

<br>

* To efficiently and quickly copy a program to a remote server and run it on the server requires commands in one line so all that needs to occur whenever you want to run a new version of the program on the server is: **press the up arrow, then press enter**.
* Commands can be strung together in a single line by seperating each command with a **semicolon**.
* To directly run commands on a remote server then exit it, surround the commands with **double quotations** i.e. **"ls"**.
* Every command needed to copy `WhereAmI.java` to the ieng6 server and run the program from your computer's terminal in a single line is:<br>`scp WhereAmI.java cs15lfa22XX@ieng6.ucsd.edu:~/; ssh cs15lfa22XX@ieng6.ucsd.edu "javac WhereAmI.java; java WhereAmI"`<br>-- *Note*: This command is only efficient if a `ssh` key has been created between your computer and the remote server.

**With this single line command, you can edit your program, save it, and run the command with just 2 keystrokes to execute your updated program on a remote server. This is illustrated in the above image.**

<br>

---
## Conclusion:

<br>

From this guide you will be able to effectivly and efficiently connect to a remote server and execute programs that you create on your computer on the remote server.