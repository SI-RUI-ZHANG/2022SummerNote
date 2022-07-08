# Creating Snapshots

## Initializing a Repository

`git init`: initiate a repository
`ls - a:` will show `.git` file
`rm -rf .git`: remove git repository
<img src="../../../images/48b583e5a607b5c877db6ba344f1d2226e989a59751637517f5f28709ffe7e31.png" style = "display: block; width: 50%; margin: auto;">

## Staging Files

- `git status:` get the status of staging area
- `git ls-files:` show files in index and working tree
- `git add file1.txt:` add file to staging area
  - `git add file1.txt, file2.txt`
  - `git add *.js`

## Committing Changes

- `git commit -m "message"`: commit with short message
  - `git commit`: default editor will show up to let us edit commit message

## Skipping the Staging area

- `git commit -a -m "message"`: committing all modified files, `-a` all
  - or `git commit -am "message"`

## Removing Files

1. `rm file2.txt`
2. `add file2.txt`
3. `git commit ...`

**or**
`git rm file2.txt`
`git rm file2.txt, file1.txt`
`git rm *.js` 

## Renaming or Moving files

1. `rm file1.txt main.js`
2. `git add file1.txt`
3. `git add main.js`
4. `git commit ...`

**or**
`git mv file1.txt main.js`

## Ignoring Files

- `.gitignore`: should be in the root of git directory
  - file listed in `.gitignore` will be ignored
  - example `echo logs/ > .gitignore`
  - already committed file will not be ignored

### To remove file only from the staging area

`git rm --cached -r bin/`

## Short Status

`git status -s:` show status in concise format
<img src = '../../../images/bba35ff67915ffbd7f6c18ed00f4a26c17d3ba15f2213502d2439efec5515c47.png' style = 'display: block; margin: auto; width: 40%'>
`A`: added
`M`: modified
`?`: untracked
<span style="color: lightgreen">green</span>: in staging area
<span style="color: red">red</span>: not in staging area

## Viewing Staged and Unstaged Changes

- `git diff --staged`: show changes made in staging area
  - repository vs staging area
- `git diff`: show changes made in working directory
  - staging area vs working directory

## Visual Diff Tools

- `git difftool --staged`
- `git difftool`

## Viewing History

- `git log`: show commit history from latest to earliest
- `git log --online`: show commit history from latest to earliest, in one line
- `git log --online --reverse`: show commit history from latest to earliest, in one line, reverse order

## Viewing a Commit
