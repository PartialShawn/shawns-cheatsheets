# My *Managing Github Projects* Notes
Some basic notes on managing Github projects: organization, configuration and common question.

## Common tasks

### Push Update
This will push everything to the master branch, I guess.

#### Okay, this doesn't seem to work in my environment
```
git config --global user.name "GitHubUsername"
```

#### This adds & updates files.
```
git add -A .
```

#### This removes files that have been deleted
(Use of add keyword is confusing to me)
```
git add -u .
```

#### Add comments
```
git commit -m "Comments here"
```

#### Push out to the server.
```
git push origin master
```

### Update local copy
This will download updates from the repository and sync your local copy

```git pull origin master```


## Create new repo
git init
git add -A .
git commit -m "initial commit"
git remote add origin _urlhere_
git push -u origin master


# Other notes

* Check out / commit
* Branching
* [Creating a release](https://help.github.com/articles/creating-releases/)
* [Adding a file](https://help.github.com/articles/adding-a-file-to-a-repository-using-the-command-line/)

## Starting A Project
* Create repo on GitHub
* [Folder configuration](https://github.com/kriasoft/Folder-Structure-Conventions)
* Commit the project via [command line](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) or [GitHub Desktop](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/) ([don't add gitignore, readme or license](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/))
* https://github.com/github/gitignore
  * [Use .gitignore](https://git-scm.com/docs/gitignore) [to hide local security configurations (config.php) and error_log](https://stackoverflow.com/a/3319626)
* [Choose a license](https://help.github.com/articles/licensing-a-repository/), and [maybe not GPL 3](https://www.cnet.com/news/torvalds-no-gpl-3-for-linux/). [Maybe not GPL](http://lucumr.pocoo.org/2009/2/12/are-you-sure-you-want-to-use-gpl/). Try [ChooseALicense.com](https://choosealicense.com/)
