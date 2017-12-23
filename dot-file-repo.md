# Creating a dot file repository #

Create a repository to apply version control to dot files in the home directory. 
This essentially follows the tutorial found [here](https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/).


## Creating the repo ##

1. Create a bare repo named ".cfg" in the home directory.
```
git init --bare $HOME/.cfg
```

2. Add the following two commands to .bashrc. 
```
alias cfg='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
cfg config --local status.showUntrackedFiles no
```
The first command replaces "git" in all commands and allows us to work with the ".cfg" repo. For example,
```
git add file.txt
git push origin master
```
would become
```
cfg add file.txt
cfg push origin master
```

3. Source .bashrc to "activate" the two commands.
```
source .bashrc
```

4. Stage the files that you wish to track.
```
cfg add file.txt
cfg add .bashrc
cfg add .gitconfig
cfg add .vimrc
...
```

5. If you accidentally add a file, you can unstage it as well.
```
cfg reset HEAD file.txt
```

6. Commit the newly added files.
```
cfg commit -m "Initial commit"
```

8. If you haven't already, create a repository on GitHub named ".cfg".
9. Create a reference to the GitHub repository from your local repository.
```
cfg remote add origin https://github.com/<your username>/.cfg.git
```

10. Pull from the remote repository.
```
cfg pull origin master
```

11. Push the local changes to the remote repository.
```
cfg push origin master
```

The GitHub repository should now contain all your selected files. 

## .gitignore ##

TODO:
add .cfg
add swps
add git and svn



## Creating a setup script ##

1. Create a GitHub gist with the following script (replacing repo URL with own)
```
#!/bin/bash/

git clone --bare https://github.com/jmcker/.cfg.git $HOME/.cfg

function cfg {
   /usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME $@
}

mkdir -p .cfg-backup
cfg checkout
if [ $? = 0 ]; then
  echo "Checked out config.";
  else
    echo "Backing up existing dot files.";
    cfg checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | xargs -I{} mv {} .cfg-backup/{}
fi;

cfg checkout
cfg config status.showUntrackedFiles no
```

2. Copy the URL of the gist.
```
https://gist.github.com/jmcker/f9ed4121dad42c3203b103c0d0f1369b
```

3. Add "/raw" to the end of the URL.
```
https://gist.github.com/jmcker/f9ed4121dad42c3203b103c0d0f1369b/raw
```

4. Visit the URL and make sure the raw gist file is served.

5. Shorten the gist + "raw" URL to something short and memorable using a service like [bit.do](bit.do).
```
Converted: 
	https://gist.github.com/jmcker/f9ed4121dad42c3203b103c0d0f1369b/raw
To:
	http://bit.do/cfg-setup-raw
```

6. Use curl (with the option to follow redirects) to download and run the setup script on any computer.
```
curl -L http://bit.do/cfg-setup-raw | /bin/bash
```

The setup script will let you quickly copy and setup the repository on a new computer.
As long as you have the cfg alias in your .bashrc, interacting with the repository should be as simple as a normal git repo.




Sources:
- https://developer.atlassian.com/blog/2016/02/best-way-to-store-dotfiles-git-bare-repo/
- https://gist.github.com/atenni/5604615
