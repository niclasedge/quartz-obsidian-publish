---
{}
---
# Introduction

Imagine that you just started a new job as a system administrator (sysadmin)
at Northwind, a high-frequency trading (HFT) firm that runs Windows on its
client computers and Linux on its server computers. Computers are the
lifeblood of the company, and you need to learn more about how to manage Linux
boxes. It's time to skill up!

Bash is the standard shell scripting language for Linux. Let's learn the
basics of Bash, starting with the syntax and commonly used commands, like `ls`
and `cat`.

## Learning objectives

In this module, you will:

  * Learn what shells are and what Bash is
  * Learn about the syntax of Bash commands
  * Learn about important Bash commands, such as `ls`, `cat`, and `ps`
  * Learn how to use I/O operators to redirect input and output
  * Learn how to update a server's operating system
  * Learn how to find and terminate rogue processes
  * Learn how to use Bash to filter Azure CLI output

## Prerequisites

  * None



---# What is Bash?

Bash is a vital tool for managing Linux machines. The name is short for "**B**
ourne **A** gain **Sh** ell."

A shell is a program that commands the operating system to perform actions.
You can enter commands in a console on your computer and run the commands
directly, or you can use scripts to run batches of commands. Shells like
PowerShell and Bash give system administrators the power and precision they
need for fine-tuned control of the computers they're responsible for.

There are other Linux shells, including csh and zsh, but Bash has become the
de facto Linux standard. That's because Bash is compatible with Unix's first
serious shell, the Bourne shell, also known as sh. Bash incorporates the best
features of its predecessors. But Bash also has some fine features of its own,
including built-in commands and the ability to invoke external programs.

One reason for Bash's success is its simplicity. Bash, like the rest of Linux,
is based on the Unix design philosophy. As Peter Salus summarized in his book
_A Quarter Century of Unix_ , three of the "big ideas" embodied in Unix are:

  * Programs do one thing and do it well
  * Programs work together
  * Programs use text streams as the universal interface

The last part is key to understanding how Bash works. In Unix and Linux,
everything is a file. That means you can use the same commands without
worrying about whether the I/O stream â the input and output â comes from
a keyboard, a disk file, a socket, a pipe, or another I/O abstraction.

Let's learn the basics of Bash, starting with the syntax and commonly used
commands, like `ls` and `cat`.



---# Bash fundamentals

An understanding of Bash starts with an understanding of Bash syntax. After
you know the syntax, you can apply it to every Bash command you run.

The full syntax for a Bash command is:

    
    
    command [options] [arguments]
    

Bash treats the first string it encounters as a command. The following command
uses Bash's `ls` (for "list") command to display the contents of the current
working directory:

    
    
    ls
    

Bash commands are often accompanied by arguments. For example, you can include
a path name in an `ls` command to list the contents of another directory:

    
    
    ls /etc
    

Most Bash commands have options for modifying how they work. Options, also
called _flags_ , give a command more specific instructions. As an example,
files and directories whose names begin with a period are hidden from the user
and are not displayed by `ls`. However, you can include the `-a` (for "all")
flag in an `ls` command and see everything in the target directory:

    
    
    ls -a /etc
    

You can even combine flags for brevity. For example, rather than enter `ls -a
-l /etc` to show all files and directories in Linux's **/etc** directory in
long form, you can enter this instead:

    
    
    ls -al /etc
    

Bash is concise. It's sometimes remarkable (and a point of pride among Bash
aficionados) how much you can accomplish with a single command.

## Get help

Which options and arguments can be used, or must be used, varies from command
to command. Fortunately, Bash documentation is built into the operating
system. Help is never more than a command away. To learn about the options for
a command, use the `man` (for "manual") command. For instance, to see all the
options for the `mkdir` ("make directory") command, do this:

    
    
    man mkdir
    

`man` will be your best friend as you learn Bash. `man` is how you find the
information you need to understand how any command works.

Most Bash and Linux commands support the `--help` option. This shows a
description of the command's syntax and options. To demonstrate, enter `mkdir
--help`. The output will look something like this:

    
    
    Usage: mkdir [OPTION]... DIRECTORY...
    Create the DIRECTORY(ies), if they do not already exist.
        
    Mandatory arguments to long options are mandatory for short options too.
      -m, --mode=MODE   set file mode (as in chmod), not a=rwx - umask
      -p, --parents     no error if existing, make parent directories as needed
      -v, --verbose     print a message for each created directory
      -Z                   set SELinux security context of each created directory
                             to the default type
          --context[=CTX]  like -Z, or if CTX is specified then set the SELinux
                             or SMACK security context to CTX
          --help     display this help and exit
          --version  output version information and exit
        
    GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
    Report mkdir translation bugs to <http://translationproject.org/team/>
    Full documentation at: <http://www.gnu.org/software/coreutils/mkdir>
    or available locally via: info '(coreutils) mkdir invocation'
    

Help obtained this way is typically more concise than help obtained with
`man`.

## Use wildcards

Wildcards are symbols that represent one or more characters in Bash commands.
The most frequently used wildcard is the asterisk. It represents zero
characters or a sequence of characters. Suppose your current directory
contains hundreds of image files, but you only want to see the PNG files; the
ones whose file names end with **.png**. Here's the command to list only those
files:

    
    
    ls *.png
    

Note

Linux has no formal concept of a file-name extension as other operating
systems do. This doesn't mean that PNG files won't have a **.png** extension.
It simply means Linux attaches no special significance to the fact that the
file names end with **.png**.

Now let's say the current directory also contains JPEG files. Some end in
**.jpg** , while others end in **.jpeg.** Here's one way to list all the JPEG
files:

    
    
    ls *.jpg *.jpeg
    

And here is another:

    
    
    ls *.jp*g
    

The `*` wildcard matches on zero or more characters, but the `?` wildcard
represents a single character. If the current directory contains files named
**0001.jpg** , **0002.jpg** , and so on through **0009.jpg** , the following
command lists them all:

    
    
    ls 000?.jpg
    

Yet another way to use wildcards to filter output is to use square brackets,
which denote groups of characters. The following command lists all the files
in the current directory whose names contain a period immediately followed a
lowercase J or P. It lists all the **.jpg** , **.jpeg** , and **.png** files,
but not **.gif** files:

    
    
    ls *.[jp]*
    

In Linux, file names and the commands that operate upon them are case-
sensitive. So to list all the files in the current directory whose names
contain periods followed by an uppercase _or_ lowercase J or P, you could
enter this:

    
    
    ls *.[jpJP]*
    

Expressions in square brackets can represent ranges of characters. For
example, the following command lists all the files in the current directory
whose names begin with a lowercase letter:

    
    
    ls [a-z]*
    

This command, by contrast, lists all the files in the current directory whose
names begin with an uppercase letter:

    
    
    ls [A-Z]*
    

And this one lists all the files in the current directory whose names begin
with a lowercase _or_ uppercase letter:

    
    
    ls [a-zA-Z]*
    

Based on all this, can you guess what the following commands will do?

    
    
    ls [0-9]*
    ls *[0-9]*
    ls *[0-9]
    

If you need to use one of the wildcard characters as an ordinary character,
you make it literal or "escape it" by prefacing it with a backslash. So, if
for some reason you had an asterisk as part of a file name â something you
should never do intentionally â you could search for it by using a command
such as:

    
    
    $ ls *\**
    



---# Bash commands and operators

Every shell language has its most-used commands. Let's start building your
Bash repertoire by examining the most commonly used commands.

## Bash commands

Let's look at common Bash commands and how to use them.

### `ls` command

`ls` lists the contents of your current directory or the directory specified
in an argument to the command. By itself, it lists the files and directories
in the current directory:

    
    
    ls
    

Files and directories whose names begin with a period are hidden by default.
To include these items in a directory listing, use an `-a` flag:

    
    
    ls -a
    

To get even more information about the files and directories in the current
directory, use an `-l` flag:

    
    
    ls -l
    

Here's some sample output from a directory that contains a handful of JPEGs
and PNGs and a subdirectory named **gifs** :

    
    
    -rw-rw-r-- 1 azureuser azureuser  473774 Jun 13 15:38 0001.png
    -rw-rw-r-- 1 azureuser azureuser 1557965 Jun 13 14:43 0002.jpg
    -rw-rw-r-- 1 azureuser azureuser  473774 Mar 26 09:21 0003.png
    -rw-rw-r-- 1 azureuser azureuser 4193680 Jun 13 09:40 0004.jpg
    -rw-rw-r-- 1 azureuser azureuser  423325 Jun 10 12:53 0005.jpg
    -rw-rw-r-- 1 azureuser azureuser 2278001 Jun 12 04:21 0006.jpg
    -rw-rw-r-- 1 azureuser azureuser 1220517 Jun 13 14:44 0007.jpg
    drwxrwxr-x 2 azureuser azureuser    4096 Jun 13 20:16 gifs
    

Each line provides detailed information about the corresponding file or
directory. That information includes the permissions assigned to it, its
owner, its size in bytes, the last time it was modified, and the file or
directory name.

### `cat` command

Suppose you want to see what's inside a file. You can use the `cat` command
for that. The output won't make much sense unless the file is a text file. The
following command shows the contents of the **os-release** file stored in the
**/etc** directory:

    
    
    cat /etc/os-release
    

This is a useful command because it tells you which Linux distribution you're
running:

    
    
    NAME="Ubuntu"
    VERSION="18.04.2 LTS (Bionic Beaver)"
    ID=ubuntu
    ID_LIKE=debian
    PRETTY_NAME="Ubuntu 18.04.2 LTS"
    VERSION_ID="18.04"
    HOME_URL="https://www.ubuntu.com/"
    SUPPORT_URL="https://help.ubuntu.com/"
    BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
    PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
    VERSION_CODENAME=bionic
    UBUNTU_CODENAME=bionic
    

The **/etc** directory is a special one in Linux. It contains system-
configuration files. You don't want to delete any files from this directory
unless you know what you're doing.

### `sudo` command

Some Bash commands can only be run by the root user; a system administrator or
superuser. If you try one of these commands without sufficient privileges, it
fails. For example, only users logged in as a superuser can use `cat` to
display the contents of **/etc/at.deny** :

    
    
    cat /etc/at.deny
    

**at.deny** is a special file that determines who can use other Bash commands
to submit jobs for later execution.

You don't want to run as root most of the time; it's too dangerous. To run
commands that require admin privilege without logging in as a superuser,
you'll preface the commands with `sudo`:

    
    
    sudo cat /etc/at.deny
    

`sudo` stands for "superuser do." When you use it, you're telling the shell
that for this one command, you're acting with the root-user level of
permission.

### `cd`, `mkdir`, and `rmdir` commands

`cd` stands for "change directory," and it does exactly what the name
suggests: it changes the current directory to another directory. It enables
you to move from one directory to another just like its counterpart in
Windows. The following command changes to a subdirectory of the current
directory named **orders** :

    
    
    cd orders
    

You can move up a directory by specifying `..` as the directory name:

    
    
    cd ..
    

This command changes to your home directory; the one you land in when you
first log in:

    
    
    cd ~
    

You can create directories by using the `mkdir` command. The following command
creates a subdirectory named **orders** in the current working directory:

    
    
    mkdir orders
    

If you want to create a subdirectory and another subdirectory under it with
one command, use the `--parents` flag:

    
    
    mkdir --parents orders/2019
    

The `rmdir` command deletes (removes) a directory, but only if it's empty. If
it's not empty, you'll get a warning instead. Fortunately, you can use the
`rm` command to delete directories that aren't empty in combination with the
`-r` (recursive) flag. The command would then look like so, `rm -r`.

### `rm` command

The `rm` command is short for "remove." As you'd expect, `rm` deletes files.
So this command puts an end to **0001.jpg** :

    
    
    rm 0001.jpg
    

And this command deletes all the files in the current directory:

    
    
    rm *
    

Be wary of `rm`. It's a dangerous command.

Running `rm` with a `-i` flag lets you think before you delete:

    
    
    rm -i *
    

Make it a habit to include `-i` in every `rm` command, and you might avoid
falling victim to one of Linux's biggest blunders. The dreaded `rm -rf /`
command deletes every file on an entire drive. It works by recursively
deleting all the subdirectories of root and their subdirectories. The `-f`
(for "force") flag compounds the problem by suppressing prompts. _Don't do
this._

If you want to delete a subdirectory named **orders** that isn't empty, you
can use the `rm` command this way:

    
    
    rm -r orders
    

This deletes the **orders** subdirectory and everything in it, including other
subdirectories.

### `cp` command

The `cp` command copies not just files, but entire directories (and
subdirectories) if you want. To make a copy of **0001.jpg** named **0002.jpg**
, use this command:

    
    
    cp 0001.jpg 0002.jpg
    

If **0002.jpg** already exists, Bash silently replaces it. That's great if
it's what you intended, but not so wonderful if you didn't realize you were
about to overwrite the old version.

Fortunately, if you use the `-i` (for "interactive") flag, Bash warns you
before deleting existing files. This is much safer:

    
    
    cp -i 0001.jpg 0002.jpg
    

Of course, you can use wildcards to copy several files at once. To copy all
the files in the current directory to a subdirectory named **photos** , do
this:

    
    
    cp * photos
    

To copy all the files in a subdirectory named **photos** into a subdirectory
named **images** , do this:

    
    
    cp photos/* images
    

This assumes that the **images** directory already exists. If it doesn't, you
can create it _and_ copy the contents of the **photos** directory by using
this command:

    
    
    cp -r photos images
    

The `-r` stands for "recursive." An added benefit of the `-r` flag is that if
**photos** contains subdirectories of its own, they too are copied to the
**images** directory.

### `ps` command

The `ps` command gives you a snapshot of all the currently running processes.
By itself, with no arguments, it shows all your shell processes; in other
words, not much. But it's a different story when you include a `-e` flag:

    
    
    ps -e
    

`-e` lists _all_ running processes, and there are typically many of them.

For a more comprehensive look at what processes are running in the system, use
the `-ef` flag:

    
    
    ps -ef 
    

This flag shows the names of all the running processes, their process
identification numbers (PIDs), the PIDs of their parents (PPIDs), and when
they began (STIME). It also shows what terminal, if any, they're attached to
(TTY), how much CPU time they've racked up (TIME), and their full path names.
Here is an abbreviated example:

    
    
    UID         PID   PPID  C STIME TTY          TIME CMD
    root          1      0  0 13:35 ?        00:00:03 /sbin/init
    root          2      0  0 13:35 ?        00:00:00 [kthreadd]
    root          3      2  0 13:35 ?        00:00:00 [rcu_gp]
    root          4      2  0 13:35 ?        00:00:00 [rcu_par_gp]
    root          5      2  0 13:35 ?        00:00:00 [kworker/0:0-cgr]
    root          6      2  0 13:35 ?        00:00:00 [kworker/0:0H-kb]
    root          8      2  0 13:35 ?        00:00:00 [mm_percpu_wq]
    root          9      2  0 13:35 ?        00:00:01 [ksoftirqd/0]
    root         10      2  0 13:35 ?        00:00:02 [rcu_sched]
    

As an aside, you might find documentation that shows `ps` being used this way:

    
    
    ps aux
    

`ps aux` and `ps -ef` are the same. This duality traces back to historical
differences between POSIX Unix systems (of which Linux is one) and BSD Unix
systems (the most common of which is macOS). In the beginning, POSIX used
`-ef` while the BSD required `aux`. Today, both operating-system families
accept either format.

This serves as an excellent reminder of why you should look closely at the
manual for all Linux commands. Learning Bash is like learning English as a
second language. There are many exceptions to the rules.

### `w` command

Users come, users go, and sometimes you get users you don't want at all. When
an employee leaves to pursue other opportunities, the sysadmin is called upon
to ensure that the worker can no longer log in to the company's computer
systems. Sysadmins are also expected to know who's logged in, and who
shouldn't be.

To find out who's on your servers, Linux provides the `w` (for "who") command.
It displays information about the users currently on the computer system and
those users' activities. `w` shows user names, their IP addresses, when they
logged in, what processes they're currently running, and how much time those
processes are consuming. It's a valuable tool for sysadmins.

## Bash I/O operators

You can do a lot in Linux just by exercising Bash commands and their many
options. But you can really get work done when you combine commands by using
I/O operators:

  * `<` for redirecting input to a source other than the keyboard
  * `>` for redirecting output to destination other than the screen
  * `>>` for doing the same, but appending rather than overwriting
  * `|` for piping output from one command to the input of another

Suppose you want to list everything in the current directory but capture the
output in a file named **listing.txt**. The following command does just that:

    
    
    ls > listing.txt
    

If **listing.txt** already exists, it gets overwritten. If you use the `>>`
operator instead, the output from `ls` is appended to what's already in
**listing.txt** :

    
    
    ls >> listing.txt
    

The piping operator is extremely powerful (and often used). It redirects the
output of the first command to the input of the second command. Let's say you
use `cat` to display the contents of a large file, but the content scrolls by
too quickly for you to read. You can make the output more manageable by piping
the results to another command such as `more`. The following command lists all
the currently running processes. But once the screen is full, the output
pauses until you select **Enter** to show the next line:

    
    
    ps -ef | more
    

You can also pipe output to `head` to see just the first several lines:

    
    
    ps -ef | head
    

Or suppose you want to filter the output to include only the lines that
contain the word "daemon." One way to do that is by piping the output from
`ps` to Linux's useful `grep` tool:

    
    
    ps -ef | grep daemon
    

The output might look like this:

    
    
    azureus+  52463  50702  0 23:28 pts/0    00:00:00 grep --color=auto deamon
    azureuser@bash-vm:~$ ps -ef | grep daemon
    root        449      1  0 13:35 ?        00:00:17 /usr/lib/linux-tools/4.18.0-1018-azure/hv_kvp_daemon -n
    root        988      1  0 13:35 ?        00:00:00 /usr/lib/accountsservice/accounts-daemon
    message+   1002      1  0 13:35 ?        00:00:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog-only
    daemon     1035      1  0 13:35 ?        00:00:00 /usr/sbin/atd -f
    root       1037      1  0 13:35 ?        00:00:00 /usr/bin/python3 -u /usr/sbin/waagent -daemon
    root       1039      1  0 13:35 ?        00:00:00 /usr/lib/linux-tools/4.18.0-1018-azure/hv_vss_daemon -n
    azureus+  52477  50702  0 23:28 pts/0    00:00:00 grep --color=auto daemon
    

You can also use files as input. By default, standard input comes from the
keyboard, but it too can be redirected. To get input from a file instead of
the keyboard, use the `<` operator. One common sysadmin task is to sort the
contents of a file. As the name suggests, `sort` sorts text in alphabetical
order:

    
    
    sort < file.txt
    

To save the sorted results to a new file, you can redirect input _and_ output:

    
    
    sort < file.txt > sorted_file.txt
    

You can use I/O operators to chain Linux commands as needed. Consider the
following command:

    
    
    cat file.txt | fmt | pr | lpr
    

The output from `cat` goes to `fmt`, the output from `fmt` goes to `pr`, and
so on. `fmt` formats the results into a tidy paragraph. `pr` paginates the
results. And `lpr` sends the paginated output to the printer. All in a single
line!



---# Exercise - Try Bash

On your own Linux computer, you can run Bash commands locally. If you have
access to Linux servers, you can remote in to them and run Bash commands
there. But nobody wants to experiment on a live production system,
particularly on their first day at Northwind.

In this unit, you'll use Azure Cloud Shell on the right as your Linux
terminal. Azure Cloud Shell is a shell you can access through the Azure portal
or at <https://shell.azure.com>. You don't have to install anything on your PC
or laptop to use it.

## Familiarize yourself with Cloud Shell

First, let's explore what's in Cloud Shell by using the Bash commands we've
learned.

  1. Use the `ls` command to list all files and subdirectories in the current directory:
    
        ls
    

  2. You should see output that looks similar to this:
    
        yourname@Azure:~$ ls
    clouddrive
    

**clouddrive** is a subdirectory of your current directory. It's a mounted
file share that persists if you're using Cloud Shell on your own account.
Right now, you're using it on the Microsoft Learn sandbox.

  3. But wait, what _is_ the current directory? Let's use the `pwd` command to find out. `pwd` stands for "print working directory." It prints out the long-form path to what directory you're in now.
    
        pwd
    

  4. You should see an output like this:
    
        yourname@Azure:~$ pwd
    /home/yourname
    

This output means that you're in a directory called **yourname** within a
directory called **home** , at the root of the Linux file system.

  5. There doesn't appear to be much in our current directory. Let's use a Bash _flag_ to print all hidden files and directories to double check that's correct.
    
        ls -a
    

  6. Whoa! That output showed us a lot more stuff in this directory than we initially thought.
    
        yourname@Azure:~$ ls -a
    .  ..  .azure  .bash_history  .bash_logout  .bashrc  clouddrive  .profile  .tmux.conf  .viminfo
    

  7. What were all of those files and subdirectories? Some are behind-the-scenes files to make Cloud Shell work. Let's discuss a few of the others.

     * `.` refers to your current directory, and `..` refers to your parent directory. Wherever you are, if you print all hidden files and directories, you'll see `.` and `..` printed.
     * `.bash_history` is a special Bash file where all commands that you enter into the shell are stored. Bash remembers your command history, which, as we'll see later, is useful.
     * `.bash_logout` is another special Bash file that is read and run every time a login shell exists. Linux superusers can modify it to customize your environment.
     * `.bashrc` is an important Bash configuration file that runs whenever you start a new shell. If you decide to open this file to look at it, be careful about making changes, because they can have unintended consequences.

## Recall your history and autocomplete commands

When you're entering complicated commands like this one, it's easy to make a
mistake:

    
    
    ls -a .azure/commands/202?*.log
    

Fortunately, Bash offers a couple pieces of functionality to help you.

### Recalling previous commands

  1. Try entering this command that has a typo (`203?` instead of `202?`):
    
        ls -a .azure/commands/203?*.log
    

  2. You should see this output letting you know that there weren't any files that matched that pattern:
    
        ls: cannot access '.azure/commands/203?*.log': No such file or directory
    

  3. Rather than entering the whole thing again to correct your mistake, you can recall previously entered commands by using the **Up arrow** and **Down arrow** keys. Try using the **Up arrow** key to bring back your incorrect command. Then use the **Left arrow key** to fix it by replacing the final `3` with a `2`. Select **Enter** again to submit the corrected command.

Using the **Up arrow** key multiple times in a row will move you back multiple
commands. Use the **Down arrow** key to move to later commands.

  4. Now you should see something like the following output. It lets you know that your command worked correctly to list files that matched the given pattern.
    
        .azure/commands/2020-01-29.21-56-35.login.103.log
    .azure/commands/2020-01-29.21-56-38.account_set.112.log
    

### Autocompletion

Let's say you want to read the contents of one of the files that you just
found. You can use the `cat` (short for "catenate") command to print the
contents of a file to the screen.

  1. To use this command, you could use the full file name, such as:
    
        cat .azure/commands/2020-01-29.21-56-35.login.103.log
    

  2. But that's a lot to type, and very error prone. Instead, you can use Bash's rudimentary autocompletion to do most of the work for you. Try typing:
    
        cat .a
    

Then select the **Tab** key. What happens?

  3. You should see the rest of the word "azure/" appear in your command:
    
        cat .azure/
    

Keep typing the beginnings of words and using **Tab** to autocomplete. Keep in
mind that if there's an ambiguity, Bash will not fill in anything. You can
select **Tab** twice to have Bash print out all the files and directories in a
given path that match the letters you've typed already.

  4. Play around until you've gotten to a real **.log** file in the command directory. Then select **Enter** to use the `cat` command to print its contents to screen. It might look something like this:
    
        CMD-LOG-LINE-BEGIN 103 | 2020-01-29 21:56:35,426 | INFO | az_command_data_logger | command args: login --identity
    CMD-LOG-LINE-BEGIN 103 | 2020-01-29 21:56:37,604 | INFO | az_command_data_logger | exit code: 0
    

Keep in mind that if you've typed an incorrect letter already, Bash will not
be able to correctly guess what letter you meant to type.

## Use `man`

We just used the `cat` command, but you don't know much about it yet. Practice
`man` to bring up more information about the `cat` command.

  1. Enter the following command to understand more about what `cat` is and how to use it:
    
        man cat
    

Yes, you entered "man cat" into your shell. Bash commands can be both cryptic
and amusing!

  2. You should see an output like this:
    
        CAT(1)                                       User Commands                                       CAT(1)
    
    NAME
           cat - concatenate files and print on the standard output
    
    SYNOPSIS
           cat [OPTION]... [FILE]...
    
    DESCRIPTION
           Concatenate FILE(s) to standard output.
    
           With no FILE, or when FILE is -, read standard input.
    
           -A, --show-all
                  equivalent to -vET
    
           -b, --number-nonblank
                  number nonempty output lines, overrides -n
    
           -e     equivalent to -vE
    
    ...
    

  3. Use up and down arrows to scroll through the manual page, and enter `q` to exit.

## Change directories

Let's practice one more basic Bash command: `cd`.

While using the shell, you're always sitting inside a directoryâjust like a
folder on your PC or Mac. To change folders, you use the `cd` (change
directory) command.

It's simple, but let's get some practice.

  1. First, enter this command to make sure you're in the right place:
    
        cd ~
    

This command moved you back to your special **home** directory in the shell,
if you weren't already there.

  2. Double check by using the `pwd` command one more time:
    
        pwd
    

  3. You should see an output like this:
    
        /home/yourname
    

`~` is another special character in Bash that refers to this home directory.
You can use `~` to refer to the location **/home/yourname** no matter where
you are in the shell.

  4. Let's change to the directory that holds log files (where we were earlier):
    
        cd .azure/commands/
    

You can either enter the full command yourself, or use **Tab** to
autocomplete.

Now you should see that the line where you enter commands looks different,
showing you where you are in the shell:

    
        yourname@Azure:~/.azure/commands$
    

  5. Try using the special `..` syntax to move up one directory:
    
        cd ..
    

Now you should be one level up in the directory structure, and your command
line should look like this:

    
        yourname@Azure:~/.azure$
    

Great work! You've taken your first steps to being a Bash expert. Let's keep
learning.

## Check your knowledge

1.

What directory would you switch to if you entered `cd .` as a Bash command?

My special "home" directory

The parent directory

The first alphabetical subdirectory

I wouldn't switch directories.

Check your answers

You must answer all questions before checking your work.



---# Exercise - Terminate a misbehaving process

Computers are imperfect. Sooner or later, something _will_ go wrong. That's
why you have a job as a sysadmin; it's up to you to troubleshoot and fix
system problems.

Imagine that a Python application is causing problems. Perhaps it's taking up
too much CPU time, or maybe it has stopped responding. In either case, you
want to stop the application. To identify a process or application, you can
use `ps` and `grep`. Then, to stop it, you can use the `kill` command. Let's
practice this in your Linux virtual machine.

## Start a misbehaving process

If you're going to kill a process, you need a process to kill. Let's create
one.

  1. Get back to your home base by typing the following command:
    
        cd ~
    

  2. In Azure Cloud Shell, enter the following command to start Linux's [`vi`](https://wikipedia.org/wiki/Vi) editor:
    
        vi bad.py
    

`vi` is a widely used text editor that Linux inherited from Unix. Love it or
hate it, a Bash user needs to know the basics of `vi`.

  3. Select the **i** key to put `vi` in insert mode. Then type in the following Python program:
    
        i = 0
    while i == 0:
        pass
    

This program, when executed, runs in an infinite loopâclearly not something
you want running on your server.

  4. Select the **Esc** key to exit insert mode. Then type the following command followed by the **Enter** key to save the program and exit `vi`:
    
        :wq
    

Be sure to include the colon at the beginning of the command. As for the
remainder of the command, `w` stands for "write" and `q` stands for "quit."

  5. Now use the following command to start the program and leave it running in the background:
    
        python3 bad.py &
    

Be sure to include the ampersand (`&`) at the end of the command. Otherwise,
you won't return to the Bash prompt. In Bash, the ampersand runs a command and
returns to the command line, even if the command hasn't finished running.

It's not obvious, but **bad.py** is now running in the background and stealing
CPU cycles from other processes. Let's take a close look at what's happening.

## Kill the process

To kill a process, you need the process name or process ID. This is a job for
`ps`.

  1. To refresh your memory, a `ps -ef` command lists all running processes and displays a great deal of information about each. Use the following command to list all running processes and filter the results to lines that contain "python":
    
        ps -ef | grep python
    

The results should look something like this:

    
        yourname+    342    254 99 23:34 pts/1    00:00:31 python3 bad.py
    yourname+    344    254  0 23:35 pts/1    00:00:00 grep --color=auto python
    

  2. From the listing, it appears that **bad.py** is consuming 99 percent of the server's CPU time. The program is living up to its name.

The `kill` command kills a running process based on its process ID. (A related
command named `killall` kills a process based on the process name.) When you
call `kill`, you have to decide what kind of "signal" to use to kill the
process. Use the following command to display a list of signal types:

    
        kill -l
    

  3. If you were killing a daemon processâone that runs in the background and provides vital services to the operating systemâyou might want to kill it and immediately restart it. To do that, you could use a `SIGHUP` signal.

In this example, you want to kill the process without restarting it.
Therefore, you want to use the `SIGKILL` signal, which corresponds to the
number 9. To that end, grab **bad.py** 's process ID from the `ps -ef` output
(it's in the second column) and use the following command to terminate the
process. Replace `PROCESS_ID` with the process ID.

    
        kill -9 PROCESS_ID
    

The same command can also be entered as `kill -s SIGKILL PROCESS_ID`. Whether
you use a signal's name or number is up to you.

  4. Finish by running `ps` again to confirm that **bad.py** is no longer running.

Another common use for `ps` and `kill` is to identify and terminate "zombie
processes," which are child processes left behind by poorly written programs.



---# Exercise - Use Bash and grep to filter CLI output

Until now, you've been running Bash commands on their own. Bash is extremely
powerful when combined with other tools, so let's get some practice by using
Bash to filter output from the Azure CLI.

  1. Let's say you want to see an up-to-date list of the VM sizes available in the westus region of Azure. You can do that with this command:
    
        az vm list-sizes --location westus --output table
    

  2. You should see a long list of VM types as an output. To narrow down this list to the VM sizes you're interested in, you can use `grep`, Linux's universal pattern-matching program. To find the "DS" sizes, popular for use in data science, use the following command:
    
        az vm list-sizes --location westus --output table | grep DS
    

This pipes output from the `az` command to `grep`, which filters out lines
that lack the "DS" string.

  3. That's still a lot of VMs. You know that DS V2 VMs are a more recent series. Let's adjust the `grep` command to use a more intricate regular expression:
    
        az vm list-sizes --location westus --output table | grep DS.*_v2
    

This filters out lines that don't match the regular expression `DS.*_v2`. You
might recognize some of the characters in that expression from our discussion
of "wildcards" in an earlier unit. Regular expressions make great use of
wildcards.

Regular expressions are a topic for another module, but come in handy for Bash
scripting.

Using Bash with other CLI commands makes the latter easier to work with. And
because a sysadmin's work never ends, any tool that reduces the workload is
welcome.



---# Knowledge check

## Check your knowledge

1.

Which of the following commands writes a list of processes associated with a
user named **scottgu** to a file?

`cat | grep scottgu > processes.txt`

`cat > grep scottgu | processes.txt`

`ps -ef | grep scottgu > processes.txt`

2.

Which of the following commands, called with the `-r` option, would you use to
delete a subdirectory that isn't empty?

`rm`

`rmdir`

`destroy`

3.

Which of the following commands combines the contents of **foo.txt** and
**bar.txt** into a new file named **foobar.txt**?

`concat foo.txt bar.txt > foobar.txt`

`cat foo.txt bar.txt | foobar.txt`

`cat foo.txt bar.txt > foobar.txt`

4.

The purpose of the `sudo` command is to:

Run a command with elevated privilege

Run a program and leave it running in the background

Prevent system files from being deleted by non-administrative users

5.

Which of the following statements is true about the command `python3 app.py
&`?

It runs **app.py** after creating a restore point in the system

It runs **app.py** and returns immediately to the command prompt

It runs **app.py** , but only if it's located in the **/etc** directory

Check your answers

You must answer all questions before checking your work.



---# Summary

In this module, you learned the basics of using Bash. Among other things, you:

  * Learned what a shell is and what Bash is
  * Learned how Bash commands are structured
  * Learned key Bash commands, such as `ls`, `cat`, and `ps`
  * Learned how to use I/O operators in Bash commands to redirect input and output
  * Learned how to find and terminate rogue processes
  * Learned how to use Bash to filter output from another CLI tool

There is much more you can do with Bash. We've gotten comfortable using Bash
as a way to interact with our shell, but you can use the commands you've
learned (and many more) to use Bash for full-fledged programming. Check out
these resources for taking your Bash knowledge to the next level:

  * [Introduction to Bash from Loyola Marymount University](https://cs.lmu.edu/%7Eray/notes/bash/)
  * [Bash Academy](https://guide.bash.academy/)
  * [Bash Guide for Beginners](http://tldp.org/LDP/Bash-Beginners-Guide/html/index.html)
  * [Learning the Shell](http://linuxcommand.org/lc3_learning_the_shell.php)
  * [Intro to Bash for chemistry students](https://erastova.files.wordpress.com/2019/09/introbash.pptx)



---