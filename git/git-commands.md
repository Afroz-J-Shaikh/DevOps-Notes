## Git Local SetUp

* Check git version

`git -v`

* If git is not installed

`sudo apt update`

`sudo apt install git`

* Setup git configuration

`git config --global user.name "your_username"`

`git config --global user.email "name@example.com"`

## Git Commands

| Command | Usage | Example |
|-------|-----------|---------|
| `git init` | initialize a repo inside directory | `git init` |
| `git clone <url>` | clone an existing repo | `git clone https://github.com/Afroz-J-Shaikh/90DaysOfDevOps.git` |
| `git add file` | add untrack files | `git add demo.txt` |
| `git commit` | make a commit | `git commit -m "added demo.txt"` |
| `git reset file` | unstrack a file | `git reset demo.txt` |
| `git status` | check if anything to commit/add | `git status` |
| `git log` | check commit history | `git log` |
| `git revert commit-id` | creates new commit that undoes changes made by given commit | `git revert 4ae73` |
| `git reset commit-id` | reset head back till given commit id | `git reset 4ae73` |
| `git branch` | list all branches | `git branch` |
| `git switch <branch>` | switch branches | `git switch feature-1` |
| `git checkout -b <branch>` | create and switch to a branch | `git checkout -b feature-2` |
| `git branch -D <branch>` | delete a branch | `git branch -D feature-2` |
| `git rebase <branch>` | creates a linear history for current branch | `git rebase master` |
| `git log --oneline --graph --all` | shows history of all branches in graph | `git log --oneline --graph --all` |
| `git stash` | stash your current changes and switch to another branch | `git stash` |
| `git cherry-pick <commit-id>` | pick and apply one commit from multiple commits to another branch | `git cherry-pick 4ae73` |
| `git merge <branch> --squash` | combine multiple commits to one and merge | `git merge feature-1 --squash` |
| `git stash pop` | get changes to working directory and deletes stash | `git stash` |
| `git stash apply` | get changes to working directory also keeps stash | `git stash` |
| `gh auth login` | login to github from cli | `gh auth login` |
| `gh auth status` | to check login status | `gh auth status` |
| `gh repo create` | creating repository | `gh repo create my-repo --public --source=. --remote=origin --push` |
| `gh repo clone username/repository` | cloning repository | `gh repo clone Afroz-J-Shaikh/90DaysOfDevOps ` |
| `gh repo list` | list all reops  | `gh repo list` |
| `gh repo delete <repo name>` | deletes a repository | `gh repo delete demo-repo` |
| `gh issue create` | create an issue | `gh issue create --title "Bug in login" --body "Login fails on invalid token"` |
| `gh pr create ` | create a pull request | `gh pr create --base main --head feature-branch --title "Add login feature" --body "Implemented login logic"  ` |
| `gh pr list` | list active pull requests | `gh pr list` |
| `gh pr merge <pr num>` | merge oull request | `gh pr merge 5` |
| `gh pr view <pr num>` | view a pull request | `gh pr view 12` |
| `gh pr review <pr num> --option` | approve/request change/comment | `gh pr review 12 --approve` |



