# Shell-Scripts

Hosting some of my utility shell scripts. Despite writing them mostly to learn how to, you might still find them useful for example to clean up auxiliary files generated when compiling *.tex documents. Either way, if you want any specific script just let me know and I'll be glad to help.

Place the scripts into ```/home/your_username/bin/```

## Clean

clean - clean - Cleans all files found from your current directory according to the argument specified. Syntax:

```
clean [-function] [-predicate]
```

Current allowed functions:

```
[-ext || -show] [-add]
```

#### -ext allowed predicates

***tex***  
Cleans all auxiliar files generated at LaTeX documents' compilation.

***java***  
Cleans all *.class files.

Notice: 
  Be careful when executing this command since you might end up removing files that are other programs need.  
  Because of this, a warning message will be displayed printing your working directory and asking for the user confirmation.

#### -show allowed predicates

***tex***  
Shows all auxiliar files generated at LaTeX documents' compilation.

***java***  
Shows all *.class files.

#### -add

Use it after any other function so that all arguments after it will be included to the extension list to look for.  
Example:  
```
clean -show tex -add xpto
```
Will also look for **\*.xpto** besides the other usual extensions.

### TODO:

~~Add ***-show*** function to display files that will be removed in case you run a deleting funciton as ***-ext***.~~  
~~Add ***-add*** funciton to allow you to add a given extension to look for.~~

## CCD

ccd - custom change directory - Changes directory to specified location.  
Imagine the following directory tree:
```
~/GitHub/Python/MyProject1/SubProject1/
```
Instead of ```cd GitHub, cd Python, ..., cd SubProject1```, ```ccd``` allows you to directly
```. ccd SubProject1```.  
Notice the use of the ```source``` indication when running the script. Thus, it is necessary to run it either as 
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

### TODO:

Add ***completition*** to directory name (that can actually be pretty useful especially since you might be cd'ing from far away).  
Do some optimization to the code, probably after ***completition*** is done.  
~~Write ```.bashrc``` function (once I get a few minutes free).~~

Ricardo Jesus
