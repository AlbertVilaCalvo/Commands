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


## Merge changes from to master remote without switching to master
// TODO


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
````


## Misc


### Prune
```
git remote prune origin
```


### Squash all commits on a branch
```
git checkout your-branch
git reset $(git merge-base master your-branch)
commit...
```
[source](https://stackoverflow.com/a/25357146/4034572)


### Always use annotated tags
```
git tag -a v1.0
````

They have extra information like author, date, SHA and message.
