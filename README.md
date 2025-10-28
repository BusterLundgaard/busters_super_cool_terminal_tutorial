# Basic, important commands:
## Navigation:
### 'cd':
Change which directory you are at in the terminal

```BASH
# go to my_cool_folder:
> cd my_cool_folder
# go to parent directory:
> cd ..
# go to the root directory:
> cd /
# go to the home directory:
> cd 
# go to the previous directory you were just at:
> cd -
# go to previous-previous directory:
> cd --
# .. and --- for third previous, and so on ...
```

## Showing files and folders:
### ls 
List the files and folders inside a directory. If no option is given, show the files and folders of the current working directory.

```BASH
# Show files in the current directory:
> ls
my_cool_folder
my_other_cool_folder
recipe.txt

# Show files inside my_cool_folder:
> ls my_cool_folder
my_cool_file.txt
```

#### Important options:
- `ls -a`: List also hidden files! (files that start with ".")
- `ls --all`: List extra information about files!
- `ls --l --human-readable`: List size information about files

### cat: print out a file
`cat`, a program frequently ridiculed for its ridicilously unintuitive name, prints out the content of a file. Its called `cat` because it can also be used to concatenate files. So to show a file we ... concatenate it with nothing. Yes. 
```BASH
# print out the contents of who_am_i.txt:
> cat who_am_i.txt
i am 
in such a good god damn mood today : D !!!

# concatenate who_am_i.txt with itself:
> cat who_am_i.txt who_am_i.txt
i am 
in such a good god damn mood today : D !!!
i am 
in such a good god damn mood today : D !!!
```

### tree
While `ls` lists the files and folders in a directory, it doesn't list the files inside the folders of that directory. `tree`, on the other hand, keeps exploring and lists out the whole tree of files and folders
```BASH
# list a tree of the current directory
> tree
.
├── plan.md
├── recordings
│   └── 2025-10-13 23-31-13.mkv
│   └── best_recordings
│   │   └── 2025-10-14 23-31-13.mkv
├── shots
│   ├── MVI_2068.MOV
└── to_produce.md

# list a tree, but only make it go one layer deep!
> tree -L 2
.
├── plan.md
├── recordings
│   └── 2025-10-13 23-31-13.mkv
│   └── best_recordings
├── shots
│   ├── MVI_2068.MOV
└── to_produce.md
```

### find
Like `tree`, find has the ability to list out _everything_ in a folder, but it lists things out in a format that ocassionally can be a bit simpler to work with: every line is just the path to a file, no details or columns like in `ls` or `tree`.

```BASH
> find
./voiceover.aup3
./manuscript2.md
./plan.md
./manuscript2 plan.md
./recordings
./recordings/2025-10-13 23-31-13.mkv
./recordings/best_recordings/2025-10-14 23-31-13.mkv
./shots
./shots/MVI_2078.MOV
./to_produce.md
```

`find` can be used in more technical ways for searching, but we wont cover that here.

## Operations on files and folders:
### touch: create files.
`touch` *creates files*. Think of a "magic _touch_" with the ability to make things appear out of thin air!

```BASH
> ls
work
notes.txt

> touch my_cool_file.txt my_other_cool_file.md
> ls
work
notes.txt
my_cool_file.txt
my_other_cool_file.md

# nothing will be displayed, because the file is empty!
> cat my_cool_file.txt
```

### mkdir: create folders
`mkdir` **m**a**k**es a **dir**ectory
```BASH
# suppose our current working directory has a folder "work" and a file "notes.txt"
> ls
work 
notes.txt 

> mkdir stuff
> ls
work
stuff
notes.txt
```

### mv: moving *and* renaming files!
`mv` is used for *moving files and folders*, as well as for *renaming files*
```BASH
> ls
work
notes.txt

# move notes.txt into the work folder:
> mv notes.txt work
# rename notes.txt to my_notes.md:
> mv work/notes.txt work/my_notes.md
# rename the folder to boring_stuff:
> mv work boring_stuff

# move a file from downloads into the current folder:
# this one is a little technical:
# "~", a tilde, refers to your home directory
# so ~/Downloads/my_downloaded_file.mp4 accesses a file inside it
# right now, you are not situated inside downloads, but some other folder
# "." is shorthand for "folder you are in right now", so we can use it to quickly move the file from downloads to where ever we are right now!
> mv ~/Downloads/my_downloaded_file.mp4 .

```

### cp
`cp` works exactly as `mv` does, but does not delete the original file; hence it just copies! 

### rm
`rm` is a pretty dangerous command. It removes a file, but removes it completely! No "trash", no undos: Your file is gone!
```BASH
> ls
work
notes.txt
stuff.txt

> rm notes.txt
> ls
work
stuff.txt

# to remove folders, we must add the -r flag. This stands for "recurse". Its a comp-sci / mathematics term meaning "keep doing the same thing again and again". In this case, that same thing is "delete everything in the folder", which we do again and again for all the folders of a folder, and so on.
> rm -r notes.txt
> ls
> stuff.txt
```

## Installing programs (depends on distribution):
### apt:
For debian-based systems such as Ubuntu, Mint, Fedora, your primary way of installing packages is through `apt`. 
```BASH
# install the illustration software inkscape: 
apt install inkscape
# remove it again
apt remove inkscape
```

### snap:
Some programs need to be installed through another manager known as snap. Programs installed through Snap run slightly differently, and a lot of larger programs like Discord and Signal run through snap, since it makes them easier to port for lazy developers like me:
```BASH
snap install discord
```

### flatpak
Flatpaks are also a way to install and run apps that again makes life easier for developers - it more or less runs on a little subsystem inside your computer, so that developers don't have to worry about differences between distributions and such.
```BASH
flatpak install sudoku
```

## Miscelannious:
### nano:
`nano` is a text editor ... in the terminal. So you can edit files from directly inside the terminal!

The controls inside `nano` are mostly intuitive, but saving and exiting can be a bit confusing at first. You save a file with CTRL-W, as in "Write". You exit with CTRL-X, as in "eXit". 

Sometimes we actually need to use nano when we want to edit a file that requires special permissions (sudo), as not all visual text editors on linux actually allow you to open them in sudo.

### sudo:
If you put `sudo` in front of a command, that command will be run with administrator priveleges - bassicly letting you do almost whatever you want. Use sudo, do not be afraid of sudo, but use it with caution - if a command requires you to use sudo, do consider that it might (or might very well not!) have significant effects on your system!

Editing files outside of your home directory usually require sudo rights. Installing programs ocasionally requires sudo rights.

```BASH
# go into root directory. We shouldn't normally make files or folders here
...
> cd /
# try to make a file:
> touch my_butt
touch: cannot touch 'my_butt': Permission denied
> sudo touch my_butt

# we've succesfully created the file! use nano to edit it:
> sudo nano my_butt
```

### history
History lists the last 500 commands you used. Can be great if you've forgotten how to do something you know you did earlier!

### man
To see the manual page for a specific command, use `man`. For example, to view the manual page for nano, i can write `man nano`. This will bring up an interactive reader (in the terminal of course) with information about nano.

### tldr
Manual pages can be pretty heavy and dense. They're great for looking up pieces of information, but not so great for understanding how to use a program in the first place. `tldr` is much better at this, as it gives you some concrete examples of things you can do with the program. 
```BASH
> tldr ls
  List files one per line:

      ls -1

  List all files, including hidden files:

      ls [-a|--all]

  List files with a trailing symbol to indicate file type (directory/, symbolic_link@, executable*, ...):

      ls [-F|--classify]
  ...
```

### unzip
`unzip` can be used to unzip files. See `tldr` for some examples of how to use it :)

### echo
Echo is an odd command that you encounter surprisingly often. It simply repeats back (prints out) what is given to it:
```BASH
> echo hello there stranger!
hello there stranger
```
`echo` can be useful when scripting, debugging, and when piping into other commands.

# Important keyboard shortcuts in the terminal:
## TAB
Whenever you have to write a file or folder name, you can simply use your TAB key to autocomplete the name for you! Suppose that i am inside a folder with the following contents:
```bash
my_cool_folder
my_other_cool_folder
recipe.txt
```
To enter `my_other_cool_folder` you could simply write "cd my_o" and press tab (either once or twice depending on your setup), and it will be autocompleted for you! This way, you dont need to remmember entire file or folder names, just their start!

Try now to write "cd my". If you press TAB now, nothing happens, since it can't distinguish between "my_cool_folder" and "my_other_cool_folder". If you press TAB one more times though, it should now show you:
```bash
my_cool_folder
my_other_cool_folder
```
so TAB completes _if_ there is only one option left. TAB-TAB shows you all options it has left for potential autocompletion.

## Copy pasting:
Copy pasting text into and from the terminal doesn't simply work with CTRL-C, CTRL-P as one may think! You actually need to use CTRL-SHIFT-C, CTRL-SHIFT-P. As you can see below, the regular CTRL-C without shift is used for something else ...

## CTRL-C
Use this to _cancel_ a command you started running.
Suppose you ran a command, say, `cp` to copy a massive directory to some location, say:
`cp -r my_massive_directory /home/buster/copy_of_my_massive_directory`
This command might take some time to run. As typical of many of these slightly unintuitive old unix commands, "no feedback is good feedback!", so `cp` gives you no feedback as it copies this large directory that might take minutes. Digressions aside, supose we regret this, and want to stop this command from copying any more. We can do this simply by pressing `CTRL-C` on our keyboards (`COMMAND-C`) for Mac i think.

## CTRL-Z
This is quite similar to 'CTRL-C', but instead of cancelling a program, it simply halts it/stops it. You can start the running process again by using `fg`, which stands for "foreground" - essentially, you've stopped it and brought it to the background, now you bring it back to the _f_ore_g_round again.

# Special symbols in the terminal:
## |: pipes
Pipes are how you make one program communicate to another. We use them *alot* in Linux. The analogy here is that as you run one program, it tends to spit out lines of output. You can "connect" this program to another with a "pipe", so that each output line flows into a program. So pipes allow us to chain programs together *one line at a time*. This is why a lot of files and programs in Linux are on so many seperate lines!

```BASH
# print out the contents of a file, then pipe it to wc to see the amount of lines, words and charachters
> cat my_file.txt | wc
10 32 230
# this file in particular seems to have 10 lines, 32 words, 230 charachters

# (think of another good example here)
```

## >: writing to files
Suppose i want to combine `my_file.txt` with `my_second_file.txt` into a new file `my_third_file.txt`. I could do this as:
```BASH
cat my_file.txt my_second_file.txt > my_third_file.txt
```
We say that > "redirects the output". Normally, the `cat` command (and most others for that matter) output their commands to the so-called "standard output", known in shorthand as "stdout". The standard output is just whatever we see on the terminal. With ">" we instead redirect the output to go into the file "my_third_file.txt". If we want to silent a command, ie, force it to not make any output, we can do something strange and "redirect it to null":
```BASH
cat my_file.txt my_second_file.txt > /dev/null
```
`/dev/null` is a special file that always deletes its own contents. Its useful then for silencing commands!

## \<: reading from files
To count lines in `my_file.txt`, we previously printed it with `cat`, then piped it into `wc`. This is wasteful actually, as we could have just given `wc` the file more directly:
```BASH
> wc < my_file.txt
10 32 230
```
The < operator reads the content of a file into a command. What's happening behind the scenes here is that < once again "redirects" a so-called "stream". Linux has, among others, a stream called standard output (the one that is printed on the terminal), and a stream called _standard input_. Programs like `wc` read from standard input and write to standard output. With < we say "take my_file.txt and _redirect_ it to standard input".

This last part isn't super important to understand, but may help intuition in the future.

## &: running something in the background
If you have a program that runs forever/continously, and you dont want it to take over your terminal completely / make it useless, you can append "&" to the end of a command:
```BASH
# obsidian is a nice note-taking app
# suppose we have a terminal open, and quickly want to run obsidian:
> obsidian

# at this point, you would now see some diagnostics/debug messages primarily meant for the developers and more technical users. Importantly though, your terminal would now be just running obsidian, and to do something else in it you would have to open a new terminal or close obsidian with CTRL-C
# we can fix this by running obsidian in the background:
> obsidian &
# yay!

# as a note, even though obsidian is no longer taking over our terminal, it is still attached to it. So closing down our terminal would also close obsidian. Dang. 
# most linux distributions come with a special program called "nohup" meant to fix this problem. We do:
> nohup obsidian &
# this is a little bit ugly and hard to remmember unfortunately :(
```

## &&: running one command right after another:
To run multiple commands, use "&&":
```BASH
# Here we both create and enter a folder in one command! I know, super cool, only on Linux.
mkdir cool_folder && cd cool_folder 
```

## \*: quickly do something to multiple files:
Wildstars, ie the funny little \*, are a super powerfull feature of the terminal that can be a little difficult to understand. Essentially they allow you to match all files that either end with something or start with something. Suppose you had:
```BASH
> ls
stuff
work
my_cool_toilet.txt
my_cool_kitchen.md
my_cool_bed.js
notes.txt
```
If you wanted to remove both `my_cool_toilet.txt`, `my_cool_kitchen.md` and `my_cool_bed.js`, you could do:
```BASH
> rm my_cool_toilet.txt my_cool_kitchen.md my_cool_bed.js
```
That's fine, but if you have _a lot of files_ you wanna delete that all share some pattern, its a little annoying. Instead, you could simply do:
```BASH
rm my_*
```
Boom! That's really all you need. Let's try to understand what's going on. Remmember the funny `echo` command from earlier? Lets check something out:
```BASH
> echo my_*
my_cool_toilet.txt my_cool_kitchen.md my_cool_bed.js
```
Remmember, `echo` just repeats back what you told it, so it must have recieved the command:
```BASH
> echo my_cool_toilet.txt my_cool_kitchen.md my_cool_bed.js
```
Essentially, whenever you use \* in a command in linux, the word that uses \* is substituted for a list of words that match. So after this subtitution, `rm my_*` really does exactly the same as `rm my_cool_toilet.txt my_cool_kitchen.md my_cool_bed.js`! 

For another example, we could concatenate/combine all `.txt` files in this folder by doing:
```BASH
> cat *.txt 
```

Wildstars are immensely useful for moving and copying many files. To move everything into the "work" folder above, i could simply do:
```BASH
> mv my* *txt work
```
As a little exercise, try to understand what the following command actually expands to :=). 

# Exercises
## Exercise set I:
- Make a folder in your home directory called "terminal_tutorial"
- Make a file in it called "my notes.txt" and write in it a bit
- Make a folder called "aarhus"
- Inside this folder, make a file called "places.txt" and write inside it some bars/places/resturaunts you like, and why. Try to have each on just one line
- View the file with cat to make sure everything has been saved correctly
- Go back to the "terminal tutorial" folder (hint: "." represents the current folder, ".." represents the folder one above you)
- Make a new folder called "cool stuff" - Note that you'll need " " to create something with spaces inside!
- copy your places.txt file over to "cool stuff"
- remove it again
- move places.txt from "aarhus" into just "terminal_tutorial"
- move "terminal_tutorial" from home into your root /. Remmember sudo!

## Exercise set II:
- Make a DEAD cow say what you wrote in "places.txt" from earlier. Remmember to consult tldr or
- Make cmatrix output letters in ~ rainbow ~ colors
- Print a tree of your root directory "/" that goes two layers deep
- Count the amount of programs you have inside /usr/bin
- Check how many files you have in your home directory that have the letter "x" inside of their names!


