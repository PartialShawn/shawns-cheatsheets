# GitHub Cheatsheet
Some basic notes on managing Github projects.

## Push Update
This will push everything to the master branch, I guess.

```
git add -A . # Add new files
git add -u . # Update existing files, removes deleted files
git commit -m "Comments here"
git push
```

Commit changes & deleted files:

```
git commit -am "comments"; git push;
```


## Start Branch

```
git checkout -b *branchname*
```

## Finished with Branch

```
git checkout master # soon to be main
git merge *branchname*
git push
```

#### Remove files
But not from local folder. This didn't seem to work.
```
git rm --cached filename # Remove file from index
git rm --cached -r foldername
```

### Update local copy
This will download updates from the repository and sync your local copy

```git pull```


## Clone repo for dev
Start a local copy of a repo for development.
```
git clone github.com/user/my-project.git .
```
Enter folder, then:

```
git config pull.rebase false
git config --global credential.helper store
```


## Create new repo for dev
git init
git add -A .
git commit -m "initial commit"
git remote add origin _urlhere_
git push -u origin master


# Other notes
* Use merge which will show when the new changes were merged in. Rebase rewinds and commits everything together on a linear history, retaining more commits, I think.
* Check out / commit
* [Use Branches](https://thenewstack.io/dont-mess-with-the-master-working-with-branches-in-git-and-github/)
* [Creating a release](https://help.github.com/articles/creating-releases/)
* [Adding a file](https://help.github.com/articles/adding-a-file-to-a-repository-using-the-command-line/)

## Starting A Project
* Create repo on GitHub
* [Folder configuration](https://github.com/kriasoft/Folder-Structure-Conventions)
* Commit the project via [command line](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) or [GitHub Desktop](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) ([don't add gitignore, readme or license](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/))
* https://github.com/github/gitignore
  * [Use .gitignore](https://git-scm.com/docs/gitignore)
  * [to hide local security configurations (config.php) and error_log](https://stackoverflow.com/a/3319626)
* [Choose a license](https://help.github.com/articles/licensing-a-repository/), and [maybe not GPL 3](https://www.cnet.com/news/torvalds-no-gpl-3-for-linux/). [Maybe not GPL](http://lucumr.pocoo.org/2009/2/12/are-you-sure-you-want-to-use-gpl/). Try [ChooseALicense.com](https://choosealicense.com/)

## Sub modules

```
git submodule add <submodule repo url> [<path/module>]
git submodule init
git submodule update

cd <path/module>
git checkout main

# or do this:
# git clone --recurse-submodules <repo>
git commit -m "add module"
git push


git submodule update --recursive --remote
git fetch
git fetch --all

git rm <path-to-submodule>
```

## Get Template

```
git remote add template [URL of the template repo]
git fetch --all
git merge template/[branch to merge] --allow-unrelated-histories
```

## Setup Authentification

Configure `~/.gitconfig` with:

```
git config --global credential.helper store
git config --global credential.useHttpPath true
```

Then when pushing you will need to enter your username and the fine grained token as your password.

Can omit `--global` if its just for the one repo.

Token must of `content` set to `read/write`.