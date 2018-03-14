## Undo

```
git reset --soft HEAD^   # keep changes
git reset --hard HEAD^   # discard changes
```

https://stackoverflow.com/a/6376039/4034572

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

### Always use annotated tags

```
git tag -a v1.0
````

They have extra information like author, date, sha and message.
