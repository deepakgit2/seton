## About Git

- Git is Distributed VCS (Version Control System) that was developed by Linus Torvalds in 2005
- Git is not an acronym. 'git' is British slang for a dumb, annoying, or generally unpleasant person.
- Git is written in C, reducing the overhead of run times associated with higher-level languages
- Git can be used with/without network connection
- Git official website is https://git-scm.com/. SCM stands for Source Code Management which means same as VCS
- There are more VCS available e.g Subversion, Mercurial, etc
- Within a VCS, project files are organized in centralized locations called repositories
- Any git project consists of three sections
  - **git directory**: Contains the history of all files and changes. Whenever we commit, git will take a snap of the whole project and will store into the git directory.
  - **working tree**: contains current state of the project including any changes we made
  - **staging area**: contains all changes that are marked to be included in the next commit.
- Flow of above three sections
  - Changes: Whenever we create a new file or modify an existing file, changes will remain in working tree only and not in staging area. We can also see these modifications using `git status` \
  Note: If a newly created directory does not contain any file recursively then it will not show as modification in `git status` command
  - Track: After modification we must track these changes by `git add`. Then only it will be a part of staging area and hence will be able to commit the changes.
  - Commit: We are ready to take a snap of the project using `git commit`. The current status of the project will be stored into the git directory.
- Git uses HEAD alias to represent the currently checked-out snapshot of our project. Simply it is a pointer to current
- Git uses SHA1 (Secure Hash Algorithm 1) to create commit id. SHA1 is not being used for security purpose instead it guarantee the consistency of our repository (means we get the exact data what we expect)
- Git is distributed VCS, distributed means that each developers has a copy of the whole repository on their local

## About GitHub

- GitHub is a remote repository hosting service for Git. Their are many more e.g BitBucket, GitLab etc.
- If you attempt to add or update a file that is larger than **50 MB**, you will receive a warning from Git. The changes will still successfully push to your repository, but you can consider removing the commit to minimize performance impact. GitHub blocks files larger than **100 MB**. To track files beyond this limit, you must use Git Large File Storage (**Git LFS**). \
**Note:** These limits are for github and not for git [tested]


## Commands

- `git add`
  - When we create any new file or copy a file to git project it will untracked by git. To track it we use this command
  - Commands
    - `git add file1.txt file2.py` It will track (if untracked) for these files and add changes into stage area
    - `git add <directory>` It will track (if untracked) for these files and add changes into stage area
    - `git add -f debug.log` Force an *ignored file* to be committed to the repository
    - `git add .` It will track (if untracked) for all project files (recursively ) and add changes into stage area
    - `git add *` similar to above command. We can use regex also.
    - `git add -p` shows the changes (patches) before adding to stage and ask weather you wanna add not not [equivalent to "git add . -p"]

- `git branch`
  - Branch is just a pointer to specific commit and series of snapshot. Git don't copy data while while creating new branch.
  - Commands
    - `git branch` list all the local branches
    - `git branch -r` list all the remote branches
    - `git branch -a` list all the branches
    - `git branch <new-branch-name>` create new branch
    - `git branch -d <branch>` delete the branch. It shows warning if didn't merge the changes
    - `git branch -D <branch>` delete the branch forcibly. It will not show any warning before deleting
    - `git branch -m <new-branch-name>` Rename the current branch to ＜new-branch-name＞

- `git checkout`
  - to check out the latest snapshot for both files and branches
  - It reverts changes to modified files before they are staged. It restores files to the latest stored snapshot, reverting any changes before staging.
  - Commands
    - `git checkout <file>` If the changes are not staged then it will store the previous staged version (or committed version if staged not available)
    - `git checkout -p` It will show the changes and ask for reverting
    - `git checkout <branch>` Switch branch
    - `git checkout -b <branch>` Create a new branch and switch to it
    - `git checkout <commit_id>` This makes your working directory match the exact state of the <commit_id> commit.

- `git clone`
  - It is used to copy a remote repository into a local workspace. *git clone* first calls *git init* to create a new repository then copies the data from the existing repository
  - Commands
    - `git clone <repo>` It will copy a remote repository into your local system (current dir)
    - `git clone <repo> <directory>` It will copy a remote repository into your local system (given directory)
    - `git clone --bare <repo>` Clone a bare version of repository.
    - `git clone -b <branch> <repo-link>` To Clone a Specific Branch
    - `git clone -depth=1 <repo-link>` Only clone the history of commits specified by the option depth=1. In this example a clone of ＜repo＞ is made and only the most recent. Shallow cloning is most useful when working with repos that have an extensive commit history.

- `git commit`
  - commit is used to save all the changes available in staging area into git directory.
  - Commands
    - `git commit -m 'your message while committing'` Inline comments otherwise it will popup nano or some other editor for commenting 
    - `git commit -a -m 'your message while committing'` It will skip the staging area and will directly apply all the changes and then commit. It will automatically stage all the changes for already tracked files but it there is any untracked file then we have to call “git add”
    - `git commit --amend` It we forgot to add any change/s in staging area while committing. We can add them later and use this command to over right previous commit (but new commit_id will be assigned). \
    Note: fixing local commit using --amend is great and after fixing it we can push it to shared repository. But *we should avoid amending commits that have already been made public*
  - Points
    - We cannot commit without a message or with empty message.

- `git config`
  - It is used to set or modify the configuration for git
  - The git config command can accept arguments to specify which configuration level to operate on which are following
    - `--local` By default, git config will write to a local level. Local level configuration is applied to current repo only. Local configuration values are stored in a following file ".git/config"
    - `--global` Global level configuration is user-specific, meaning it is applied to an operating system user. Global configuration values are stored in following file "~/.gitconfig" and for windows its "C:\Users\\.gitconfig"
    - `--system` System-level configuration is applied across an entire machine. This covers all users on an operating system and all repos. 
  - Commands
    - `git config --global user.email "me@gmail.com"` to set global user email for all repository in that system
    - `git config --global user.name "my name"` to set global user name for all repository in that system
    - `git config -l` show the config
    - `git config --global credential.helper cache` It enables to store your credential for a time period (default 15 min). We have enter password one time only for any commands that require password e.g `git pull`. We can also use the SSH key-pair to store the credentials.
    - `git config credential.helper 'cache --timeout=3600'` Increase the timeout (support in seconds). If you would like the daemon to exit early, forgetting all cached credentials before their timeout we can use `git credential-cache exit`
    - `git config --global alias.co checkout` We can use `git co` as shortcut for `git checkout` and similarly br: branch, ci: commit, st: status, etc. more details can be found here [git-alias](https://www.atlassian.com/git/tutorials/git-alias)

- `git diff`
  - It shows the changes that are in staged area
  - Commands
    - `git diff` shows the un-staged change for tracked files only [equivalent to "diff -u" linux command]
    - `git diff --staged` shows the changes that are staged and not committed
    - `git diff <branch1> <branch2>` Comparing branches
    - `git diff <branch1> <branch2> ./diff_test.txt` To compare a specific file across branches

- `git fetch`
  - It is use to retrieve the changes from remote repo to locally. 
  - Commands
    - `git fetch` fetches remote updates but doesn't merge we have to merge the updates manually (using "git merge origin/master") and resolve conflicts (if any)

- `git init`
  - It creates a new Git repository. It can be used to convert an existing, unversioned project to a Git repository or initialize a new, empty repository. Most other Git commands are not available outside of an initialized repository, so this is usually the first command you'll run in a new project.
  - It creates “.git” subdirectory in current location which is the database for our git project that stores the changes and change history.
  - Commands
    - `git init` Initialize an empty git repository in current directory.
    - `git init <directory>` Initialize an empty git repository in the specified directory.
    - `git init --bare <directory>` Initialize a bare repository. Conventionally, bare repositories initialized with the --bare flag end in .git

- `git log`
  - show the commit history
  - Commands
    - `git log` show all commit in pagination format
    - `git log -2` It show last 2 commits
    - `git log -p` It is used to show the more details about the commit. It shows the patch (-p) that was used for commit
    - `git log --author="<pattern>"` Search for commits by a particular author. The  argument can be a plain string or a regex.
    - `git log --grep="<pattern>"`  Search for commits with a commit message that matches pattern
    - `git log <file>` Only display commits that include the specified file.
    - `git log --stat` shows the file wise changes (how many lines add/removed)
    - `git log --merge` log with a list of commits that conflict between the merging branches.
    - `git log origin/main` todo
    - `git log --graph --oneline --all`

- `git merge`
  - Both branches are pointed at the same commit when we merge two branches
  - fast-forward & three-way merge
  - Commands
    - `git merge <branch>` First we checkout to master branch then execute this command.
    - `git merge --abort` It will exit from the merge process and return the branch to the state before the merge began.

- `git pull`
  - It’s an easy way to synchronize your local repository with upstream changes. This is the same as `git fetch ＜remote＞` followed by `git merge origin/＜current-branch＞`
  - Commands
    - `git pull` Default invocation of git pull will is equivalent to *git fetch origin HEAD* and *git merge HEAD* where HEAD is ref pointing to the current branch.
    - `git pull <remote>` Fetch the specified remote’s copy of the current branch and immediately merge it into the local copy. 
    - `git pull --no-commit <remote>` Similar to the default invocation, fetches the remote content but does not create a new merge commit.
    - `git pull --rebase <remote>` Same as the above pull Instead of using *git merge* to integrate the remote branch with the local one, use *git rebase*

- `git push`
  - Git push is most commonly used to publish an upload local changes to a central repository. After a local repository has been modified a push is executed to share the modifications with remote team members.
  - Commands
    - `git push <remote> <branch>` Push the specified branch to, along with all of the necessary commits and internal objects. By default, Git chooses origin as remote & current branch as branch to push i.e `git push origin main`
    - `git push <remote> --all` Push all of your local branches to the specified remote.
    - `git push -u <remote> <branch>` push new branch to remote which is newly created
    - `git push --delete <remote> <branch>` To delete the remote branch

- `git rebase`
  - This is use to rebase, squash, change order of commits, etc.
  - If we want to make a change to a remote branch, we must do following i.e Pull the remote branch, merge it with the local branch, then push it back to its origin.
  - Commands
    - `git rebase <base>` This automatically rebases the *current/checkout branch* onto ＜base＞. If we wanna change base of feature-branch the first call `git checkout feature-branch` and followed by `git rebase main` command
    - `git rebase -i` It opens interactive rebase. Where using commands e.g pick, squash, etc we can squash, change order of commits and so on
      - For squashing two commits into one. First we call `git rebase -i main/master` then we will write following in text editor. We may have to use `git push -f` if those two commits are already push to remote
        ```
        pick 3e5ty First commit
        squash 9a1zu second commit
        ```
      - `git rebase -i HEAD\~3` need to explore

- `git remote`
  - There is a name assign to remote repos by default its **origin**
  - If we want to make a change to a remote branch, we must do following i.e Pull the remote branch, merge it with the local branch, then push it back to its origin.
  - Commands
    - `git remote -v` To show the configuration (fetch & push url) for remote repo. Usually fetch & push url are same but sometime can be different
    - `git remote show origin` It shows more info about remote repo
    - `git remote update` get the contents of a remote branch without automatically merging [todo]

- `git reset`
  - It is the counter part of "git add" and revert the changes that are staged
  - Commands
    - `git reset HEAD <file>` <span style="color:red">todo</span>
    - reset can be used during a merge conflict to reset conflicted files to a know good state

- `git revert`
  - It is one of the rollback method which create new commit (that is inverse of a particular commit)
  - Commands
    - `git revert HEAD` It create new commit which is the inverse changes of latest commit.
    - `git revert <commit-id>` It create new commit which is the inverse changes of particular commit. **Note:** It only revert the changes that were made in that particular commit and not after that.

- `git rm/mv`
  - It works similar to linux "rm/mv" commands. Only difference is that if we use "rm/mv" we have to call "git add" on the other hand if we use "git rm/mv" changes will automatically move to staging area. We must use "git rm/mv" as it has more advantages also [need to check https://stackoverflow.com/questions/7434449/why-use-git-rm-to-remove-a-file-instead-of-rm]
  - Commands
    - `git rm file1.txt file2.txt` use to delete the file/s also supports regex
    - `git mv /path/to/file1.txt /path/to/file2.txt` use to rename or move the files
    - `git rm --cached [filename/s or pattern]` use to stop tracking a file that is currently tracked

- `git show`
  - Similar to 'git log' but for viewing the specific commit
  - Commands
    - `git show` It will show the latest commit log
    - `git show <commit id>` It will show the info about the specific commit
    - `git show <commit id>:<filepath>` It will show the historic version of the file during that <commit id>

- `git status`
  - It is used to get information about working tree and pending changes


## Concepts
- **Bare Repositories**
  - Bare repository are same as normal repo that doesn’t have a working directory (.git folder). We cannot edit files and commit changes in that bare repo. We would create a bare repository to *git push* and *git pull* from, but never directly commit to it.
  - For using git commands on bare repo we need to pass bare repo path e.g `git clone /path/to/bare_repo`
  - The most common use case for bare repo is to create a remote/central repository. Conventionally, bare repo name ends with ".git". Github or Gitlab repo are can also be considered as bare repo. 
  - We can think of --bare as a way to mark a repository as a storage facility, as opposed to a development environment. This means that for virtually all Git workflows, the central repository is bare, and developers local repositories are non-bare.

- **Conflicts**
  - If the two branches you're trying to merge both changed the same part of the same file, Git won't be able to figure out which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually. When you encounter a merge conflict, running the `git status` command shows you which files need to be resolved.
  - When Git encounters a conflict during a merge, It will edit the content of the affected files with visual indicators that mark both sides of the conflicted content. These visual markers are: <<<<<<<, =======, and >>>>>>>. It's helpful to search a project for these indicators during a merge to find where conflicts need to be resolved. Generally the content before the ======= marker is the receiving branch and the part after is the merging branch.
  - Think of these new lines as "conflict dividers". The ======= line is the "center" of the conflict. All the content between the center and the <<<<<<< HEAD line is content that exists in the current branch main which the HEAD ref is pointing to. Alternatively all content between the center and >>>>>>> new_branch_to_merge_later is content that is present in our merging branch.
  - Once you've identified conflicting sections, you can go in and fix up the merge to your liking. When you're ready to finish the merge, all you have to do is run git add on the conflicted file(s) to tell Git they're resolved. Then, you run a normal git commit to generate the merge commit.


- **Forking**
  - A way of creating a copy of the given repository so that it belongs to our user.
  - Typical workflow of contributing in a project
    - Create Fork of that project. Then it will reflect into your github
    - Make the changes
    - Create a pull request for that. Owner of that repo can accept/reject this pull request.

- **gitignore**
  - If there are some files that you never want to commit. It's too easy to accidentally commit them (especially if you use git add . to stage all files in the current directory). That's where a .gitignore file comes in handy. It lets Git know that it should ignore certain files and not track them.
  - We can place a .gitignore file in the root directory and put some files or pattern which you don't wanna track
    ```python
    # used for commenting in .gitignore files
    filename.ext # ignores file with name (filename.ext) in repository [recursively]

    any_directory/ # to ignore entire directory just include /
    any_directory/subdirectory to ignore entire directories # to ignore entire sub directories
 
    *.log # to ignore all .log files [recursively]
    !example.log # we can use a prefix of ! to negate a file that would be ignored [recursively or in any subdirectory]

    debug?.log # A question mark matches exactly one character.
    debug[0-9].log # Square brackets can also be used to match a single character from a specified range.
    debug[01].log # Square brackets match a single character form the specified set.
    debug[!01].log # An exclamation mark can be used to match any character except one from the specified set.
    debug[a-z].log # Ranges can be numeric or alphabetic.
    ```
  - Points
    - Git will not ignore the file if you've already committed (but ignore if a file is only tracked and not committed) it. You'll have to untrack the file first, then it will start ignoring it `git rm --cached <file>`
    - Git sees every file in your working tree as one of three things: tracked, untracked and ignored
    - If you’re having trouble, you can find out why certain files are being ignored by using the `git check-ignore -v <file>`
    - Explore more .gitignore patterns [here](https://www.atlassian.com/git/tutorials/saving-changes/gitignore)

- **Merge and Rebase**
  - Merge: There are two type of merge that git perform which are following
    - Fast Forward merge (or 1-way merge)
      - A fast-forward merge can occur when there is a linear path from the current branch tip to the target branch. Instead of “actually” merging the branches, all Git has to do to integrate the histories is move (i.e., “fast forward”) the current branch tip up to the target branch tip. [Pictorial View of Fast Forward Merge](https://www.atlassian.com/git/tutorials/using-branches/git-merge#:~:text=Fast%20Forward%20Merge&text=3%2Dway%20merges%20use%20a,tips%20and%20their%20common%20ancestor.)
    - 3-way merge
      - However, a fast-forward merge is not possible if the branches have diverged. When there is not a linear path to the target branch, Git has no choice but to combine them via a 3-way merge. 3-way merges use a dedicated commit to tie together the two histories. The nomenclature comes from the fact that Git uses three commits to generate the merge commit: the two branch tips and their common ancestor. [Pictorial View of 3-Way Merge](https://www.atlassian.com/git/tutorials/using-branches/git-merge#:~:text=Fast%20Forward%20Merge&text=3%2Dway%20merges%20use%20a,tips%20and%20their%20common%20ancestor.)
  - Rebase: 3-way merge create a split history and its very hard find a bug with the diverge history. So we use rebase instead of merge it keeps history clean
    - Rebasing is the process of moving or combining a sequence of commits to a new base commit. Rebasing is most useful and easily visualized in the context of a feature branching workflow. [Pictorial View of Rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase#:~:text=What%20is%20git%20rebase%3F&text=From%20a%20content%20perspective%2C%20rebasing,them%20to%20the%20specified%20base.)

- **Pull Request**
  - A commit or series of commits that you send to the owner of the repository so that they incorporate it into their tree
  - If we raised a pull request and we got notified that it require more changes then we can simply make changes in our branch and push them it will automatically reflect in the same pull request. If we wanna different PR then need to create other branch for that.

- **Remote**
  - Remote repositories are versions of your project that are hosted on the Internet or network somewhere. You can have several of them, each of which generally is either read-only or read/write for you.
  - There is a name assign to remote repos by default its **origin**
  - We can have more than one remote, `git remote -v` command lists them all.
  - Remote branches are read only. We can not modify them directly. If we want to make a change to a remote branch, we must do following i.e Pull the remote branch, merge it with the local branch, then push it back to its origin.
  - If a new branch is added on remote we can use `git pull` to fetch and merge all changes. But new branch will not be reflected locally unless we call `git checkout <new-branch-name>`
  - We can have more than one remote, `git remote -v` command lists them all.



## Resources
- https://git-scm.com/book/en/v2 This book (available online and in print) covers all the fundamentals of how Git works and how to use it. Refer to it if you want to learn more about the subjects that we cover throughout the course.
- https://git-scm.com/docs/gittutorial This tutorial includes a very brief reference of all Git commands available. You can use it to quickly review the commands that you need to use
- https://git-scm.com/doc Official git docs [\*]
- https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud Git Interactive tutorial with visualization [\*]
- https://thoughtbot.com/blog/5-useful-tips-for-a-better-commit-message
- https://docs.github.com/en/get-started GitHub Documentation
- https://training.github.com/downloads/github-git-cheat-sheet.pdf Github cheat-sheet
- http://google.github.io/styleguide/ google coding style guide
- https://medium.com/osedea/the-perfect-code-review-process-845e6ba5c31 
- https://github.github.com/gfm/ markdown formatting 


## Terminologies
- VCS: Version Control System


## To-Do
  - [git-stash](https://www.atlassian.com/git/tutorials/saving-changes/git-stash)
  - [git-blame](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-blame)
  - [git-tag](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-tag)
  - [undoing-changes](https://www.atlassian.com/git/tutorials/undoing-changes)
  - https://randomblog.hu/setting-up-git-for-ubuntu-with-autocompletion add git autocompletion in docker
  - https://www.coursera.org/learn/it-security/item/P1I8z  Cryptography in Action 

<!-- available username
dsinghub
dsingh66
dsingh88 -->
