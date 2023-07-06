
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

> This would allow us to use `init` command
```sh
alias init="git init && git add . && git commit -m 'init'"
```

> Allow us to use `git set-remote` command
```sh
git config --global alias.set-remote '!f() { GIT_USER=$(gh api user | jq -r .login); REPO_NAME=$(basename $(pwd)); git remote add origin git@github.com:$GIT_USER/$REPO_NAME.git; }; f'
```

## Workflow

```sh
cargo lambda new function
cd function
init
git set-remote
```