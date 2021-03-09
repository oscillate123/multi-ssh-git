Multiple SSH Keys settings for different github account
=================================================================


create different public key
---------------------------------

create different ssh key according the article [Linux & Mac & Windows Set-Up SSH with Github](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account)

	$ ssh-keygen -t rsa -C "your_email@youremail.com"

for example, 2 keys created at:

	~/.ssh/id_rsa_thor
	~/.ssh/id_rsa_ironman

then, add these two keys as following

	$ ssh-add ~/.ssh/id_rsa_thor
	$ ssh-add ~/.ssh/id_rsa_ironman

you can delete all cached keys before

	$ ssh-add -D

finally, you can check your saved keys

	$ ssh-add -l


Modify the ssh config
---------------------------------

	$ cd ~/.ssh/
	$ touch config
	$ subl -a config

Then added

	#thor account
	Host github.com-thor
		HostName github.com
		User git
		IdentityFile ~/.ssh/id_rsa_thor

	#ironman account
	Host github.com-ironman
		HostName github.com
		User git
		IdentityFile ~/.ssh/id_rsa_ironman


Clone you repo and modify your Git config
---------------------------------------------

clone your repo
	git clone git@github.com:thor/gfs.git repo-folder

cd repo-folder and modify git config

	$ git config user.name "thor"
	$ git config user.email "thor@gmail.com" 
 
	$ git config user.name "ironman"
	$ git config user.email "ironman@gmail.com" 

or you can have global git config
	$ git config --global user.name "thor"
	$ git config --global user.email "thor@gmail.com"

and change `[remote "origin"]`/`url` field in your local `.git/config` to use the `Host` defined in `.ssh/config`

```
[remote "origin"]
        url = git@github.com`-thor`:thor/gfs.git
```

then use normal flow to push your code

	$ git add .
	$ git commit -m "your comments"
	$ git push


Another related article in Chinese

1. http://4simple.github.com/docs/multipleSSHkeys/

Sources:
https://support.cloudways.com/using-git-command-line-ssh/
https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account
https://docs.github.com/en/github/authenticating-to-github/error-permission-to-userrepo-denied-to-userother-repo
