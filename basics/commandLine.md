
# Command-line Stuff
# Basic commands 
[`pwd`](#pwd)  
[`ls`](#ls)  
[`mkdir`](#mkdir)  
[`cd`](#cd)  
[`touch`](#touch)  
[`rm`](#rm)  
[`echo`](#echo)  
[`cat`](#cat)  
[Pipes and redirection `( > | < )`](#pipes-and-redirection)  

# Things to note 
[Wrap Spaces](#wrap-spaces-in-names-in-quotes)  
[Escape Spaces](#escape-spaces-in-names)  
[Removing Folders](#removing-folders)  
[Shells](#shells)

# `pwd` 
Stands for '__P__ rint __W__ orking __D__ irectory'  
Useful when your terminal doesn't show you the working (current) directory  
`$> pwd`
```
D:\Dev\VisualStudio\ExServer\ExServer
```

# `ls`
Stands for __L__ i __S__ t  
### 1.  Plain Usage
`$> ls`
```
App.config  Etc/             FodyWeavers.xsd  MainForm.cs           obj/             Properties/
bin/        ExServer.csproj  Libs/            MainForm.Designer.cs  packages.config
Core/       FodyWeavers.xml  Macros/          MainForm.resx         Program.cs
```
`ls` Can also be used to list content within a directory without changing directory  
### 2. Listing a path
`$> ls Core`
```
Client.cs  Data/  Logging.cs  Noise/  RPCMessage.cs  Server.cs  Service.cs  Services/  Utils/  VersionInfo.cs
```
`$> ls Core/Services`  
```
CoreService.cs  DBService.cs  DebugService.cs  LoginService.cs  MapService/  SyncService.cs
```
### 3. Flags
Can also be used with some flags to change the output.  
These flags can be used regardless of the presense of the path to list.  
Adding the `-l` flag will show the output in a __L__ ong list:  
`$> ls Core/Data -l`
```
total 28
-rw-r--r-- 1 ninja 197609 23263 Sep  3 09:41 SimplexNoise.cs
-rw-r--r-- 1 ninja 197609  3012 Sep  3 09:41 UberData.cs
```

Adding the `-a` flag will show __A__ ll files and folders (including hidden files/folders), if there are any:  
`$> ls Core/Data -a`
```
./  ../  SimplexNoise.cs  UberData.cs
```

They can be combined if desired, as well as placed before the path.  
`ls -al Core/Data`
```
total 32
drwxr-xr-x 1 ninja 197609     0 Sep  3 09:41 ./
drwxr-xr-x 1 ninja 197609     0 Nov 11 11:37 ../
-rw-r--r-- 1 ninja 197609 23263 Sep  3 09:41 SimplexNoise.cs
-rw-r--r-- 1 ninja 197609  3012 Sep  3 09:41 UberData.cs
```
### 4. Help
There are other flags as well, for more info use `ls --help`

# `mkdir`
stands for __M__ a __K__ e __DIR__ ectory.  
Creates a directory with the name(s) given to it.  
Say we are in an empty directory
### Plain Usage
`$> ls`
```
(no output)
```
`$> mkdir ayy lmao`
```
(no output)
```
(Actually made two directories!)  
`$> ls`
```
ayy/  lmao/
```
If we want to make a directory with a space in the name, we have two options:


### Wrap spaces in names in Quotes

Wrap the name in quotes:  
`$> ls`
```
(no output)
```
`$> mdkir "ayy lmao"`
```
(no output)
```
`$> ls`
```
'ayy lmao'/
```


### Escape spaces in names
Escape the space in the name with `'\'`:

`$> ls`
```
(no output)
```
`$> mdkir ayy\ lmao`
```
(no output)
```
`$> ls`
```
'ayy lmao'/
```

# `cd`
Stands for '__C__ hange __D__ irectory'.  
Changes the current working directory  based on the given path  
Names still have the same restrictions as with `mkdir`, and need to be closed  
using all of the above folders:  
`$> pwd`
```
D:\Dev\examples
```
`$> ls`
```
 ayy/  'ayy lmao'/   lmao/      
```
`$> cd ayy`
```
(no output)
```
`$> pwd`
```
D:\Dev\examples\ayy
```

# `touch`
Doesn't stand for anything.  
Creates a file with the name provided to it  
`$> ls`
```
(no ouput)
```
`$> touch test.txt`
```
(no output)
```
`$> ls`
```
test.txt
```

# `rm`
Stands for '__R__ e __M__ ove'  
Removes something from the file system.

`$> ls`
```
test.txt  yep/      
```
`$> rm test.txt`
```
(no output)
```

### Removing Folders 
In order to remove folders, a `-r` (__R__ ecursive) flag needs to be added  
`$> ls`
```
yep/
```
`$> rm yep`
```
rm: cannot remove 'yep\': Is a directory
```
`$> rm -r yep`
```
(no output)
```

# `echo`
Echo. Echo. Echo.  
`echo` repeats what was passed into it.  
`$> echo hello world`
```
hello world
```

# `cat`
Stands for con __CAT__ enate  
This dumps the content of the file it is run on.  
`$> cat file`
```
(everything in file)
```

# `wc`
Stands for __W__ ord __C__ ount
Counts the number of lines, words, and characters in a file.  
`$> wc file`
```
(lines words characters) file
```

# Pipes and Redirection (`> | <`)
Data from one program can be sent into another, or into a file.  
For example, if we want to take the output of a command and store it in a file...

# Redirect into file `>`

`$> mkdir blah`
```
(no output)
```
`$> ls > outfile.txt`
```
(no output)
```
`$> ls`
```
blah/  outfile.txt
```
It has created a file that stores the output of that command.

`$> cat outfile.txt`
```
blah/
outfile.txt
```
(Notice that we ran `ls`, and the output file was created before the `ls` command ran, as the `outfile.txt` shows up in that listing)

---
# Pipe `|`

Some files may be really long, so you could combine `cat` with a pipe, and send the data to a page viewer, like `more` or `less` (`more` is an easier program to start with, `less` is an advanced `more`)

Say, to view this file in the command line- this file is pretty long by now, so it will scroll by very quickly. Try both of these:  

`$> cat commandLine.md | more`  
you can then view the file one line at a time (enter)  
or a page at a time (space)

---

# Redirect into program `<`
This redirects a file's content into a program  
Notice the subtle difference between the following:  
`$> wc < outfile.txt`
```
(lines words characters)
```
`$> wc outfile.txt`
```
(lines words characters) outfile.txt
```

Some programs may be able to open a file and read input, but they know where the data comes from, and may change their behavior if they have that information.  
Passing data by `<` changes the way the program recieves the information.

### shells
Note that different shells (the program that actually runs your commands) may behave differently. Different operating systems have different shells available, and not all of them will act exactly the same.
