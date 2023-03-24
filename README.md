# Shell-tab-renamer-for-my-Ubuntu

Small script to change the name of your shell tab when it's created.

Place the .rename.cfg file in your home directory (or elsewhere but beware of the source command).

Add theses 2 lines in your .bashrc.

```shell=
source ~/.renamer.cfg
PS1=$(titre $PS1)
```

Change the values of $tab and $suffixes in the .rename.cfg file.


Once of my bigest issue with Ubuntu is the unavailability to change the name of shell tabs.
Recently, instead of being serious at work, I'decided to do some research and try to fix this. That's how I ended up with this project

### How does it works : 

We're gonna modify a environment variable : PS1
This variable contains the username / hostname / working directory informations displayed at each prompt.
PS1 looks like \u@\h:\w$ with \u for username, \h for hostname and \w for working directory. We can see that the symbols in PS1 are in the prompt, for exemple, mine is dova@Dovabuntu:~$
In reality PS1's composed of the folowing 
```
\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$" 
We can perceive the \u, \h and \w.
```


We can add the box ```\[\e]2;${title}\a\] ```at the end of PS1 to change the tab name. Credits to Thibault Baheux author of __this post__ https://www.it-connect.fr/linux-comment-renommer-son-terminal/ for finding this.
So you can create a variable title and all of your tabs will now be named according to it.

But we can add more chaos in there.
We will create a list of strings that can ramdomly be chosen as a title at the creation of the tab.

To get a random element from the list, we're gonna use this command 
``` shell
${list[RANDOM%${#list[@]}-1]}.
```

We got all the elements that we need to implement our function.






There's a bonus function in the .rename.cfg file that can add a suffix to your username. This function can be easily edited to add a suffix/prefix to any tag.

If you want to add this function, add this line in addition to the others.


```shell=
source ~/.renamer.cfg
PS1=$(titre $PS1)
PS1=$(addSuffix $PS1)
```
