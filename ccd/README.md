## CCD

ccd - custom change directory - Changes directory to specified location.  
Imagine the following directory tree:
```
~/GitHub/Python/MyProject1/SubProject1/
```
Instead of ```cd GitHub, cd Python, ..., cd SubProject1```, ```ccd``` allows you to directly
```. ccd SubProject1```.  
Notice the use of the ```source``` when running the script. Thus, it is necessary to run it either as 
```
. ccd <dir_name> or source ccd <dir_name>
``` 
or change the ```~/.bashrc``` file.  
In order for this to work add the following code to your ```~/.bashrc```:  
```
ccd(){
. ccd "$@"
}
```
And have the script in the usual ```~/bin/ or /bin``` directory.  
In case you use this ```.bashrc``` trick you can simply run the script as:  
```
ccd <dir_name>
```

#### Completion
In order to enable tab completion you need to copy the code at the completion directory to ```/etc/bash_completion.d/ccd``` (use ```nano, vim``` or something similar, and fill free to skip the comments). After that once you open a new shell session you should have tab completion enabled to ```ccd```.  
You can use completion with or without using ```crontab```. I myself prefere with ```crontab``` as I get less hangs during system start ups (actually I get no hangs with ```cron``` since the heavy duty runs threaded). Further instructions available at each of the OS's folders.

**Notice:** ~~Since new version, using folders with names should work. This also means that a portion of the code became redundant and so I decided to edit the old function which did the parse of directories which were fed by the old complete rules. Now it shouldn't be needed and thus should work with less code. In any case for now I left the old function commented at least until I run some more debug.~~ Since I rewrote most of the code (specially these implementations) this is no longer true. Directories with spaces onto their names should work natively with very little issues to it, and even those cases are mostly caught. ~~The biggest problem with names right now is as ```ccd``` completion won't complete "Hello World XPTO" if you also have another directory called "Hello World". I'm looking into ways of fixing this.~~ This is now fixed.

### TODO:

~~Add ***completion*** to directory names (that can actually be pretty useful especially since you might be cd'ing from far away).~~  
~~Do some optimization to the code, probably after ***completition*** is done.~~  
~~Write ```.bashrc``` function (once I get a few minutes free).~~  
~~Do some clean up to the code, and add greater support to the usage of folders with spaces. Partially done.~~
Mac OSX support.

Ricardo Jesus
