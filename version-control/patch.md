# Git patches

- Useful if want to save current local staged changes instead of commiting them
  - why
    - want to give to another dev to work on, esp for remote pairing
    - Commiting and pushing might lead to unfinished code being used by another dev
    - The CI build might fail, people will not be able to checkout code until build passes

## Via Intellij

- Very simple, just use the gui

## Command line

If you haven't yet commited the changes, then:

`git diff > mypatch.patch`

But sometimes it happens that part of the stuff you're doing are new files that are untracked and won't be in your git diff output. So, one way to do a patch is to stage everything for a new commit (git add each file, or just git add .) but don't do the commit, and then:

`git diff --cached > mypatch.patch`

Add the 'binary' option if you want to add binary files to the patch (e.g. mp3 files):

`git diff --cached --binary > mypatch.patch`

Can also use // better to use

`git diff HEAD > file_name.patch`

You can later apply the patch:

`git apply mypatch.patch`

Note: You can also use `--staged` as a synonym of `--cached`.

### Creating patches for commits

### Issues
