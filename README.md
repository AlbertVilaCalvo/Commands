Just a few commands ;)

* [Git](#Git)
* [npm](#npm)
* [Yarn](#Yarn)
* [Homebrew](#Homebrew)
* [Oh My Zsh](#Oh-My-Zsh)
* [Android](#Android)
* [React Native](#React-Native)
* [hosts file](#hosts-file)
* [Gradle](#gradle)
* [Prettier](#prettier)

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

## Revert the changes done on a file (or files) in a branch, so that it's content is the same than develop or master

`git checkout <branch> -- <filename>`

Eg: `git checkout develop -- buildsystem/versions.gradle`

This leaves in the staging area the changes that bring the file to the same contents than develop. You need to commit then.

Note that you can put as many files as you want: `git checkout <branch> -- <filename> ... <filename>`

[source1](https://stackoverflow.com/q/215718/4034572) [source2](https://stackoverflow.com/q/1817766/4034572)

## View file line history/changes

Show the changes from line 135 to 140:

`git log --pretty=short -u -L 135,140:file/path/something.txt`

[source](https://stackoverflow.com/a/19757493/4034572)

## GitHub pull request

https://gist.github.com/Chaser324/ce0505fbed06b947d962

http://blog.davidecoppola.com/2016/11/howto-contribute-to-open-source-project-on-github/

```
git remote add upstream git@github.com:Kotlin/kotlinx.coroutines.git
```

### Incorporating upstream changes
```
git fetch upstream master
git log --oneline --graph --decorate --all
git checkout master`
git merge upstream/master
git push origin master
```

## Misc

### Remove untracked files
```
git clean -f -d
```

### Prune
```
git remote prune origin
```

### See commit differences between two branches
```
git log master..feature-branch
```
If you've already switched to `feature-branch` you can use `git log master..`.

[source](https://stackoverflow.com/q/13965391/4034572)

### Squash all commits on a branch
```
git checkout your-branch
git reset $(git merge-base master-or-develop your-branch-name)
```
This leaves all changes on the branch at the staging area. Then you can `git add .` and `git commit`.

[source](https://stackoverflow.com/a/25357146/4034572)

### Stash with message
```
git stash push -m "Some message"
```
https://git-scm.com/docs/git-stash

### Always use annotated tags
```
git tag -a v1.0
```

They have extra information like author, date, SHA and message ([more info](https://stackoverflow.com/q/4971746/4034572)).

### Search string on git history
```
git log -S something
git log -p -S something
```

[source](https://stackoverflow.com/a/4472267/4034572)

### Remove carriage return

If you see `^M` run `sed -i.bak $'s/\r//' filename` (with backup) or `sed -i '' -e $'s/\r//' filename` (no backup).

[source](https://stackoverflow.com/a/21622340/4034572)


# npm

CLI docs: https://docs.npmjs.com/cli-documentation/

Tip: `npm run` lists all the executable commands/scripts.

Upgrade npm itself:

`npm install npm@latest -g`

(If this command fails and we then get `zsh: command not found: npm` we can fix it with `brew reinstall node`.)

List global pacakges:

`npm list -g --depth=0`

List outdated global packages:

`npm outdated -g`

Add global package:

`npm install -g <package>`

Upgrade global package:

`npm update -g <package>`

Remove global package:

`npm uninstall -g <package>`


# Yarn

CLI docs: https://classic.yarnpkg.com/en/docs/cli/

Tip: `yarn run` lists all the executable commands/scripts.

To upgrade yarn itself use Homebrew.

Know which version of a package you are using:

`yarn list @react-native-community/cli`

Upgrade all packages to latest:

`yarn upgrade --latest`

## Global

List global packages:

`yarn global list`

Add global package:

`yarn global add <package>`

Upgrade global packages one by one (lists all packages and versions and allows to choose):

`yarn global upgrade-interactive --latest`

Upgrade global packages all at once:

`yarn global upgrade`

Remove global package:

`yarn global remove <package>`


# Homebrew

https://docs.brew.sh/FAQ

https://docs.brew.sh/Manpage

```
brew update --debug --verbose
brew outdated
brew upgrade
brew cleanup
```

## Fix `zsh: command not found: yarn`

Run `brew doctor`. If you see:

```
Warning: You have unlinked kegs in your Cellar.
Leaving kegs unlinked can lead to build-trouble and cause brews that depend on
those kegs to fail to run properly once built. Run `brew link` on these:
  yarn
```

Then run `brew link yarn`, which may fix the issue. If you then get `Error: Could not symlink bin/yarn. Target /usr/local/bin/yarn already exists.`, then follow the instructions or run `brew link --overwrite yarn`.

## Fix not using the latest yarn version installed by brew

If `brew info yarn` gives a different (higher) version than `yarn -v` then run `brew link --overwrite yarn`. If you then see:

```
Warning: Already linked: /usr/local/Cellar/yarn/1.22.4
To relink:
  brew unlink yarn && brew link yarn
```

Then run `brew unlink yarn && brew link yarn`. If you then see `Error: Could not symlink bin/yarn. Target /usr/local/bin/yarn already exists.`, then follow the instructions or run `brew link --overwrite yarn`.

## Cask

List of commands: https://github.com/Homebrew/homebrew-cask/blob/master/USAGE.md

```
brew cask install <package>
brew list --cask
brew outdated --cask
brew upgrade --cask
```


# Oh My Zsh

https://github.com/ohmyzsh/ohmyzsh

https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git

Upgrade: `omz update`


# Android

List emulators: `emulator -list-avds`

List emulators running ('List of devices attached'): `adb devices`

Launch emulator: `${ANDROID_HOME}/emulator/emulator -avd Nexus_5X_API_27_-_Google_Play &`

Emulator show touches: `adb shell settings put system show_touches 1`

Emulator hide touches: `adb shell settings put system show_touches 0`

## Test deep links

https://developer.android.com/training/app-links/deep-linking#testing-filters

`adb shell am start -W -a android.intent.action.VIEW -d "scheme://example.com/some-path" com.example.debug`

If you have multiple emulators then add '-s emulator-name', like this:

`adb -s emulator-5554 shell am start -W -a android.intent.action.VIEW -d "scheme://example.com/some-path" com.example.debug`

## Modify the emulator `hosts` file

https://medium.com/code-procedure-and-rants/use-modified-hosts-file-on-android-emulator-4f29f5d12ac1

https://stackoverflow.com/questions/41117715/how-to-edit-etc-hosts-file-in-android-studio-emulator-running-in-nougat

Note: you need to use the `${ANDROID_SDK_ROOT}/emulator/emulator`, like this:

`${ANDROID_SDK_ROOT}/emulator/emulator -avd Pixel_2_API_19_4.4_KitKat_-_1080x1920_5inch_xxhdpi -writable-system &`

where `ANDROID_SDK_ROOT` is `/Users/albert/Library/Android/sdk` [source](https://stackoverflow.com/a/52496987/4034572)


# React Native

Show dev menu: `adb shell input keyevent 82` or `adb shell input keyevent KEYCODE_MENU`


# hosts file

`hosts` file is located in `/private/etc`

https://github.com/StevenBlack/hosts

```
cd ~/Informàtica/hosts
ggpull
python3 updateHostsFile.py [--backup]
```

## Error ModuleNotFoundError: No module named 'requests'

If an error like "ModuleNotFoundError: No module named 'lxml'" is thrown when running `updateHostsFile.py`, then install the required dependencies by following [Generate your own unified hosts file](https://github.com/StevenBlack/hosts#generate-your-own-unified-hosts-file).

Basically run `pip3 install --user -r requirements.txt`.


# Gradle

Docs: https://docs.gradle.org/current/userguide/userguide.html

DSL reference: https://docs.gradle.org/current/dsl/index.html

CLI: https://docs.gradle.org/current/userguide/command_line_interface.html

Basic help: `./gradlew help`

CLI options/help: `./gradlew --help`

## Wrapper

Upgrade the wrapper: `./gradlew wrapper --gradle-version=6.7.1`

This updates gradlew, gradlew.bat, gradle/wrapper/gradle-wrapper.jar and gradle/wrapper/gradle-wrapper.properties.

After upgrading `./gradlew --version` should show the new version.

## Tasks

List tasks: `./gradlew tasks` or `./gradlew Task :help`. Note that this does not list all the tasks. To see 'Other tasks' run `./gradlew tasks --all`.

Run task: `./gradlew <task>`. To see what it would do if run do `./gradlew <task> --dry-run`, which shows the tasks dependencies that would be executed.

Task help: `./gradlew help --task <task>`

## Clean

`./gradlew clean`

`./gradlew cleanBuildCache` - [Doesn't work on Android](https://stackoverflow.com/a/43245885/4034572)

Clear Gradle global cache (when clean and 'Invalidate Caches / Restart' don't work):
```
ls ~/.gradle/caches/
rm -rf ~/.gradle/caches/build-cache-*
```

Clear local .gradle folders:
```
find . -type d -name ".gradle"
find . -type d -name ".gradle" -exec rm -rf {} +
```

### Deep clean

https://github.com/rock3r/deep-clean

```
find . -type d -name "build"
find . -type d -name "build" -exec rm -rf {} +

find . -type f -name "*.iml"
find . -type f -name "*.iml" -exec rm -rf {} +

find . -type d -name ".idea"
find . -type d -name ".idea" -exec rm -rf {} +
```

## Profile

About `--profile` on the [docs](https://docs.gradle.org/current/userguide/command_line_interface.html#sec:command_line_performance):

>  Generates a high-level performance report in the `$buildDir/reports/profile` directory. `--scan` is preferred.

You can do `./gradlew --profile` or `./gradlew clean build --profile`. On Android you can do `./gradlew assembleDebug --profile`.

## Daemon

https://docs.gradle.org/current/userguide/gradle_daemon.html

Enabled by default since 3.X. Always enable the daemon since it makes builds start faster (JVM startup time is bad). To do so add `org.gradle.daemon=true` to `gradle.properties`.

> Gradle will kill any Daemon that has been idle for 3 hours or more, so you don’t have to worry about cleaning them up manually.

List daemons: `./gradlew --status`

Kill daemons: `./gradlew --stop`

https://docs.gradle.org/current/userguide/gradle_daemon.html#sec:how_can_i_stop_a_daemon

> Daemon processes will automatically terminate themselves after 3 hours of inactivity or less. If you wish to stop a Daemon process before this, you can either kill the process via your operating system or run the `gradle --stop` command. The `--stop` switch causes Gradle to request that all running Daemon processes, _of the same Gradle version used to run the command_, terminate themselves.


# Prettier

https://prettier.io/docs/en/install.html

```
npm install --save-dev --save-exact prettier

echo {}> .prettierrc.json

touch .prettierignore
```

> Tip! Base your .prettierignore on .gitignore and .eslintignore.

Note that it ignores files located in `node_modules` directory - [docs](https://prettier.io/docs/en/cli.html#--with-node-modules)

Run: `npx prettier --write .`

Check: `npx prettier --check .`

## Options

```
{
  "semi": false,
  "singleQuote": true
}
```

`semi: false` - Only add semicolons at the beginning of lines that may introduce ASI failures - [docs](https://prettier.io/docs/en/options.html#semicolons)

`singleQuote: true` - Chooses the one which results in the fewest number of escapes, but in case of a tie or the string not containing any quotes, defaults to _single_ quotes - [docs](https://prettier.io/docs/en/options.html#quotes) - [rationale](https://prettier.io/docs/en/rationale.html#strings)

## WebStorm setup

https://prettier.io/docs/en/webstorm.html

https://www.jetbrains.com/help/webstorm/prettier.html

Go to Preferences | Languages and Frameworks | JavaScript | Prettier.
Check 'On code reformat' and 'On save'. Modify glob pattern to `{**/*,*}.{js,ts,jsx,tsx,css,json}`.

Reformat with Prettier: ⌥⇧⌘P
