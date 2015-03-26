## CCD

ccd - custom change directory - Changes directory to specified location.  
Imagine this directory tree:
```
~/GitHub/Python/MyProject1/SubProject1/
```
Instead of ```cd GitHub, cd Python, ..., cd SubProject1``` (or ```cd GitHub/Python/.../SubProject1/```), ```ccd``` allows you to directly ```ccd SubProject1```.  

### Instructions

**1.** Copy the script inside your OS's folder to whatever location you want, though I suggest you place it inside a directory such as ```~/bin/```. Anyway, check that that's a valid location for saving and running scripts, so that you can just type the script's name and have it run. You can do that by typing ```echo $PATH``` to the terminal and check what directories are listed there. If ```~/bin``` is there, I strongly advise you to save the script there.  

**2.** You want this script as executing a command inside you current shell instance. I mean, usually what you get when you run ```find ~ -name something``` is a new shell to span (which you don't see, but that happens on the background), and then the output of that shell is shown to your usual standart out, which is actually by default the first shell that spanned the one that actually run the script, in this case, ```find```. You can look at it as some sort of a matryoshka. Nonetheless, this doesn't work well when you are running something as a ```cd``` from a script. Think of it, the shell which you are writing to gets a ```cd``` command from within a script, what does it do? It spans a new shell to take care of it, and waits for the output. The spanned shell does her job and changes directory to whatever you specified, but still, there is nothing to output so she doesn't output a thing. Thus, she closes, and your mother shell is left with no changes (the actual change of directory is done on the child shell, which is shutdown once she completes her job). Another example of a command that have to be called sourced if he is run from within a script is the ```pushd``` (and ```popd``` of course). But you have a solution, which is to source your script to the "mother shell" directly, which is done (and for the ```ccd```) by typing ```source ccd <dir_name>``` or ```. ccd <dir_name>```. The ```.``` is an alias for ```source```, and has nothing to do with the location of the script.  
You should now be able to use ```ccd``` by calling it as ```. ccd <dir_name>```.  

**3.**
Still, if you don't like this solution (as I don't), do the following to avoid specifing that the script is to run sourced:  
On the terminal, run ```nano ~/.bashrc``` and to the openned file save the code  
```
ccd(){
. ccd "$@"
}
```
which is simply a function that runs sourced by default (as it is called from the ```.bashrc``` file, which itself calls the actual script ```ccd```). Simple but effective. Now you only need to run ```ccd <dir_name>```. That's better.  
You should now be able to run ```ccd``` simply as ```ccd <dir_name>```.  

**4.** Completion means you are able to write a portion of a word and have it magically completed by pressing the ```tab``` key. It's a pretty neat perk that Unix systems usually have to run commands on terminals and such. I thought that would be something honestly useful on this script (usually path completion is awesome, any completion is awesome actually), so I added a simple rule that should be enough to make that ```tab``` work. If you are interested in enabling it, inside each of the OS's folders there is a folder called ```completion``` that has the instructions to do so.  

If you did this, you should now have ```ccd``` script running simply as ```ccd <dir_name>``` where you can actually just type ```ccd <dir_[tab]``` to get your ```dir_name```. If you don't please let me know and I'll happily look into it. 
<!--
#### Completion
In order to enable tab completion you need to copy the code at the completion directory to ```/etc/bash_completion.d/ccd``` (use ```nano, vim``` or something similar, and fill free to skip the comments). After that once you open a new shell session you should have tab completion enabled to ```ccd```.  
You can use completion with or without using ```crontab```. I myself prefere with ```crontab``` as I get less hangs during system start ups (actually I get no hangs with ```cron``` since the heavy duty runs threaded). Further instructions available at each of the OS's folders.
-->
**Notice:** ~~Since new version, using folders with names should work. This also means that a portion of the code became redundant and so I decided to edit the old function which did the parse of directories which were fed by the old completion rules. Now that shouldn't be needed and thus should work with less code. The biggest problem with names right now is as ```ccd``` completion won't complete "Hello World XPTO" if you also have another directory called "Hello World". I'm looking into ways of fixing this.~~ This has now been fixed.

### TODO:

~~Add ***completion*** to directory names (that can actually be pretty useful especially since you might be cd'ing from far away).~~  
~~Do some optimization to the code, probably after ***completition*** is done.~~  
~~Write ```.bashrc``` function (once I get a few minutes free).~~  
~~Do some clean up to the code, and add greater support to the usage of folders with spaces. Partially done.~~  
Mac OSX support.

**CCD does not completly work for Mac OSX yet.**

Ricardo Jesus
