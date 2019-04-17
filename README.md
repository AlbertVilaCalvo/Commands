Just a few commands ;)

* [Git](#Git)
* [npm](#npm)
* [Yarn](#Yarn)
* [Homebrew](#Homebrew)
* [Oh My Zsh](#Oh-My-Zsh)

man pages: https://tldr.sh/

# Git

## Undo
```
git reset --soft HEAD^   # keeps changes
git reset --hard HEAD^   # discards changes
```
[source](https://stackoverflow.com/a/6376039/4034572)


### Undo a public commit
```
git revert HEAD
```


## Merge changes from remote master branch to a feature branch without switching to master
```
> git checkout some-branch
> git fetch origin # gets you up to date with origin by getting all commits on all branches, but named 'origin/branch'
> git merge origin/master # brings all commits in 'origin/master' to whatever branch we are; we could use --ff-only
> git fetch origin master:master # update master if we have a feature branch checked out
```
[source-part-1](https://stackoverflow.com/a/20103414/4034572)
[source-part-2](https://stackoverflow.com/a/17722977/4034572)

## GitHub pull requests
```
git remote add upstream git@github.com:Kotlin/kotlinx.coroutines.git
```


### Incorporating upstream changes
```
git fetch upstream master
git log --oneline --graph --decorate --all
git checkout master
git merge upstream/master
git push origin master
```


## Misc


### Prune
```
git remote prune origin
```


### Squash all commits on a branch
```
git checkout your-branch
git reset $(git merge-base master your-branch)
```
This leaves all changes on the branch at the staging area. Then you can `git add .` and `git commit`.

[source](https://stackoverflow.com/a/25357146/4034572)


### Always use annotated tags
```
git tag -a v1.0
```

They have extra information like author, date, SHA and message ([more info](https://stackoverflow.com/q/4971746/4034572)).

### Search string in all git history
```
git log -Spassword
```

[source](https://stackoverflow.com/a/4472267/4034572)


# npm

Upgrade npm itself:

`npm install -g npm`

List global pacakges:

`npm list -g --depth=0`

List outdated global packages:

`npm outdated -g`

Add global package:

`npm install -g <package_name>`

Upgrade global package:

`npm update -g <package_name>`

Remove global package:

`npm uninstall -g <package_name>`


# Yarn

To upgrade yarn itself use Homebrew!

List global packages:

`yarn global list`

Add global package:

`yarn global add <package_name>`

Upgrade global packages one by one:

`yarn global upgrade-interactive`

(lists all packages and versions and allows to choose)

Upgrade global packages all at once:

`yarn global upgrade`

Remove global package:

`yarn global remove <package_name>`


# Homebrew

https://docs.brew.sh/FAQ

# Oh My Zsh

Upgrade: just type `upgrade_oh_my_zsh` :)
