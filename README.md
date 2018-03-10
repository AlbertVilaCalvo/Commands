
# GitHub pull requests

```
git remote add upstream git@github.com:Kotlin/kotlinx.coroutines.git
```

## Incorporating upstream changes

```
git fetch upstream master
git log --oneline --graph --decorate --all
git checkout master
git merge upstream/master
git push origin master
````


