# Getting started with git A virsion control system

Configure user information

``` bash
git config --global user.name "your-name"
git config --global user.email "youremail@example.com"
```

Initialising a new repository 
Navigate to the project directory and execute:
```bash 
git init
```

To clone an existing repository the command is:
```bash
git clone https://github.com/username/repository.git
```

The day-to-day operations in git primarily involves creating, editing, staging, and committing files. The workflow usally follows this pattern:

1. Make chages to your project file.
2. Stage the changes, preparing them for a commit:
```bash
git add <filename>
```
or, stage all modified files:
```bash
git add . 
```

3. Committing the staged changes to the repository's history:
```bash
git commit -m "commit message describing the chages made"
```

4. Add remote github repo 
```bash
git remote add origin https://github.com/username/repo.git
```

5. push the files to the repo
```bash
git push -u origin main
```

Branching and Merging 
Creating new branch is achieved with:
```bash
git branch <branchname>
```

Switching to your new branch is done via:
```bash
git checkout <branchname>
```

merging incorporate the changes from one branch to another, typically into master branch after the feature is completed or fix is verified
```bash 
git merge <branchname>
```

Pushing local changes to remote repository is done with:
```bash
git push origin <branchname>
```

Fetching update from the remote repository and merging them into your local branch
```bash
git pull
```