### Completion

Completion, regarding most Unix systems, is the capability of having some word completed by simply pressing the ```tab``` key. Since I find it a very useful mechanism, I decided to add a simple rule to make it work for ```ccd```.  
Completion usually works by generating a list of possible matches, and once you press the ```tab``` key three situations can occur:  
 - Either there is only one match that completes your query (even if partially) and thus it is completed right away;  
 - There is more than one match, and thus by pressing the ```tab``` key again fast enough you are promped with the list of all possible matches;  
 - There is no match, in which case pressing the ```tab``` does nothing.  

Since the generated list of matches for this specific script is quite big (it's all of your available directories (not including hidden ones), starting from you ```~/``` directory onwards), I was getting a few seconds of delay when opening the terminal for the first time after a start-up, or after some heavy work which pushed the cached list out of RAM. Anyway, to overcome this issue I wrote a very simple function which only saves this list to a file saved under your ```/tmp/``` directory. I did this because parsing entries of a file to an array is much faster than actually looking for the entries and then parse them. Moreover, the way I implemented it let's the process run on the background, from time to time, so that your work is not affected at all from it. Now, this is possible using an utility called ```cron``` that runs scheduled tasks, and which is probably already shipping with your current Linux distro. If it is, I strongly advise you to use this, since ```cron``` is waking up every minute with you without any jobs to do, so it does no harm to have it run a small script, for example daily. Otherwise, I will explain how to get around ```cron``` and enable completion to ```ccd``` without it.

**1.** Decide whether you want to automate the list generation with or without ```cron```. Again, it you have ```cron``` already installed on your distro, you have very little reasons not to use it.  

**2.** (Skip this if not using ```cron```)  
Run ```crontab -e``` in the terminal. If this is your first time using ```cron``` you will be promped to choose a text editor to use by default (any will do).  
After choosing one, go to the end of the file that was opened and add the following lines:  
```
@reboot ~/.bashrc "saveDirs" &
@daily ~/.bashrc "saveDirs" &
```
The script ```saveDirs``` does not exist yet, but we will take care of that later. Still, the first line enable the script to run at every system start-up, so that as soon as the system boots you have a fresh list of your directories. Besides, that process is run threaded, so you won't even notice it. The second line, actually feel free to replace ```@daily``` with whatever time description you want. It simply makes it so that at the time specified there, the list of directories gets updated. I chose to make it update on a daily basis, still if you want it to be updated every 10 minutes for example just change it to ```*/10 * * * * ~/.bashrc "saveDirs" &```.  
Save the file and make sure your rules were added by running ```crontab -l```. If you are displayed with rules you specified, you are set for the next stage.  

**3.** Now, run ```nano ~/.bashrc``` and copy to it the code bellow:  
```
saveDirs(){
    find $HOME \( ! -regex '.*/\..*' \) -type d -printf "%f\n" 2>/dev/null | sort | uniq > /tmp/ccd.txt
}
```
After that, close the terminal window, open a new one and try to run ```saveDirs```. If you manage to do that, you should have the list generating script ready. To be extra sure, run ```cat /tmp/ccd.txt```. If you get a list full of directory names (some of which you might recognise, others you probably won't), in that case the script is running properly and you can procced to the next step.  

**4.** Now, you only actually need to set the completion script. In order to do this, run ```sudo nano /etc/bash_completion.d/ccd```, and save to there the code at the ```ccd``` file given in this folder. Save the file, close the terminal window and open it once again.  
Now, just try to have some word completed by pressing the ```tab``` key. For example, in my case if I type ```ccd [tab][tab]``` (where ```[tab]``` denotes the ```tab``` key being pressed), I currently get a message asking me if I want all the 1180 possible completions being listed. If you get such a big number (or close), odds are everything is working fine.  
Congratulations on finishing all the set up needed to make this script fully working! Hope it deserves the effort.  

***Notice:*** On the folder old you will find an old version of the ```ccd``` completion rule. You can use it if you don't want to add the ```saveDirs``` to your ```.bashrc``` but I advise against using it, since not only does it seem more prone to erros but is also not as good. Still, that's your decision.  

Ricardo Jesus
