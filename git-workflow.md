
## Pre-requisite
- git cli
- gh cli
- bash scripts / git alias

## Login to github

```sh
gh auth login
```

> Example when you are prompted
```sh
? What account do you want to log into? GitHub.com
? You're already logged into github.com. Do you want to re-authenticate? Yes
? What is your preferred protocol for Git operations? SSH
? Upload your SSH public key to your GitHub account? /Users/username/.ssh/id_rsa.pub
? Title for your SSH key: GitHub CLI
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: 6156-DAC5
Press Enter to open github.com in your browser...
✓ Authentication complete.
- gh config set -h github.com git_protocol ssh
✓ Configured git protocol
✓ SSH key already existed on your GitHub account: /Users/username/.ssh/id_rsa.pub
✓ Logged in as Username
```

## Create Bash Script / Git Alias

> This would allow us to use `git start` command
```sh
git config --global alias.start '!git init && git add . && git commit -m "init"'
```

> Allow us to use `git repo` on the function / folder and will create the remote repository

```sh
git config --global alias.repo '!gh repo create $(basename $(pwd)) --public'
```

> Allow us to use `git set-remote` command
```sh
git config --global alias.set-remote '!f() { GIT_USER=$(gh api user | jq -r .login); REPO_NAME=$(basename $(pwd)); git remote add origin git@github.com:$GIT_USER/$REPO_NAME.git; }; f'
```

> Allow us to push to main on init with this command `git upstream`
```sh
git config --global alias.upstream 'push --set-upstream origin main'
```
> Add submodule using folder path with command `git module FOLDERNAME`
```sh
git config --global alias.module '!f() { GIT_USER=$(gh api user | jq -r .login); REPO_NAME=$1; git submodule add git@github.com:$GIT_USER/$REPO_NAME.git $REPO_NAME; }; f'
```

> Delete a submodule of lambda folder with command `git unmodule FOLDER_NAME`

```sh
git config --global alias.unmodule '!f() { REPO_NAME=$1; git submodule deinit -f -- $REPO_NAME; rm -rf .git/modules/$REPO_NAME; git rm -f $REPO_NAME; }; f'
```

> Delete an alias with `git unalias ALIAS_NAME`
```sh
git config --global alias.unalias '!f() { git config --global --unset alias.$1; }; f'
```

> Delete a remote repository with `git delete`
```sh
git config --global alias.delete '!f() { gh repo delete $(basename $(pwd)) --yes; }; f'
```
Note: to use this command you need to add `delete_repo` scope by running this command

```sh
gh auth refresh -h github.com -s delete_repo
```
## Workflow

```sh
cargo lambda new my-function
cd my-function
git start
git repo
git set-remote
# check if git remote url is set
# git remote -v
# push code to remote repository
git upstream
# go back to main repo
cd ..
# run this if it is your first submodule
# git submodule init
git module my-function
git add .gitmodules my-function
git commit -m "added new module"
```
