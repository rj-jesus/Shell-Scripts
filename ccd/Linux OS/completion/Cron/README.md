### Using Cron

Since the completion of this script is quite resources demanding I've decided to include a kind of "cached aproach" to this. With this in mind I've used ```cron``` to automate the creation of a file with the full list of available directories. This is still in it's early stages, as I test this funcitonality I'll update the log above.  
As a side note, all files here are related to completion jobs. Thus, the file named ```ccd``` is not actually the script. Only the file with the rules for the completion.

#### CRON Log

~~Still in early development. Not usable.~~  
As of now, completion with cron works with no seen bugs. In order to enable it, do the following:  
```
~$ crontab -e
```  
You should be promped to choose a text editor. Any will work of course. After that, had the following jobs to the file you are displayed:  
```
@reboot ~/bin/saveDirs &
*/12 * * * * ~/bin/saveDirs &
```  
And have the script ```saveDirs``` at your usual ```~/bin``` directory (I might add some functionality to it later).  

This will make that, at system start-up, a file with all the possible completions is generated (the process runs threaded and it's pretty fast so it shouldn't be a problem). After that, every (in this case) 12 minutes the rules are updated (in case you create new directories or whatnot). Still, you can change this value to whatever you want. This also runs threaded.  
After this is done, you should have a working completion scheme for ```ccd``` (given that you updated the completion rule on ```/etc/bash_completion.d```. I myself prefer this to the old completion scheme as it loads values on the background to your needs. Otherwise I was getting a few terminal hangs as the system first loaded the values. After that they were cached to RAM and thus it wasn't an issue, but I didn't like that hang. It wasn't polished. This runs much better in my opinion, I encourage you to try it. Any bugs please let me know (cron can be quite picky since he uses some different system variables).

Ricardo Jesus