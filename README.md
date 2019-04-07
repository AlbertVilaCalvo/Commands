Just a few commands :)

* [Git](#Git)
* [npm](#npm)
* [Yarn](#Yarn)
* [Homebrew](#Homebrew)

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
