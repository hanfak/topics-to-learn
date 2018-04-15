# Version Control - Git

I have mainly been using Git to version control all software that has been worked on. There are some legacy projects that has used 'Subversion' but these have been migrated to Git.

## Commands

- add
- commits
  - messages inline
  - via terminal text editor ie vim
    - common vim controls
      - https://stackoverflow.com/questions/6098742/using-git-commit-a-with-vim
- shelf & unshelf
- Tag
- revert
- reset
- diff
- logs/history
- push
- pull
- fork
- clone
- fetch
- patch
- stash
- branch
  - checkout
- merge
- rebase
- cherry pick

### Links

- [Git Documentation](https://git-scm.com/doc)
- https://www.tutorialspoint.com/git/index.htm
- Tutorial
  - https://git-scm.com/docs/gittutorial
  - https://www.atlassian.com/git/tutorials
  - https://try.github.io/levels/1/challenges/1
  -

## Git In Intellij

Most of my git usage is done via Intellij. Here are some common uses and tips:

- shortcuts (unix)
  - ctrl + k = commit
  - F7 or alt + left/right = go through changes
  - ctrl + shift + k = push
  - alt + ??: To access Version control window
- On commit screen, click on optimise imports on right hand side
    - can do ctrl + alt + o when in a particular file
  - There is a link (see pic) where you can see prior commits (commit message history ctrl + m ), great if need to see history of commits or copy commit messages
- All the files ticked which need to be added
  - Can untick files not to be part of commits
    - Be careful, as when close commit window and bring it up it will select all added files for commit
- Use ```revert``` on a file if need to undo all changes back to last commit instead of lots of undos
- Use shelf to save changes in case need to do another design or fix a bug
- In version control window > local changes, can move files from different default changeset (which will commited ) to another change set
- In version control window > log, great place to do searching through history of commits, view files that were commited, view diff of files with current file or another previous commit
  - Great to see visual representation of branches and where they were merged
  - To make full use of this feature, good to have a naming strategy for commits
    - ie ```<Story number> <developers working on commit> description of changes in commit```
  - Can create branches, revert, reset, checkout branches
- Make use of patches, help to save changes in file, and can be passed to different machines or saved for when story mgiht be played at later date as it has been put on hold.
  - best to use name of patch as the same as the commit message
  - Can also turn shelf into a patch
    - In version control window > Shelf section
- Use of VCS > local history
  - Great for going through multiple changes that have been made


## Git Repository


- Types
  - Github
  - Gitlabs
  - Bitbcket (little experience)
- Remote
  - Delete
  - Add
  - view all remotes
- Permissions
- Create project/repo
- Connecting via
  - SSH
  - Https
- README.md
  - Creating Documentation
  - writing in markdown
  - https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
  - https://dbader.org/blog/write-a-great-readme-for-your-github-project

### Links

- https://guides.github.com/introduction/flow/
- https://guides.github.com/
- https://help.github.com/

## Continuous Integration

How work is integrated into shared repository

- Types
  - Master branch (current way)
    - General format
      - Make sure repo is up to date (git pull and rebase)
      - work on Master
      - When commiting, run full build and test suite
      - When green commit and push
        - If there is a new commit to pull, cannot push with out pulling
        - Need to merge changes into local, get passing build and push
          - Normally work on stories that are on separate parts of same code base, but different pairs would work on different apps so no merge issues
  - Branching for each user story
    - General format
      - create branch from master
      - add commits for this story
      - Make pull request when story is completed
      - Code is reviewed and changes takes place (code review)
      - Merge branch with master
    - When Used
      - no pairing takes place thus reviewing code is a must

- Merging

### Links

- https://www.thoughtworks.com/continuous-integration
- https://martinfowler.com/bliki/FeatureBranch.html
- https://martinfowler.com/articles/continuousIntegration.html
- Tutorial
  - https://learngitbranching.js.org/
  - https://www.atlassian.com/git/tutorials/using-branches
  - https://docs.microsoft.com/en-us/vsts/git/tutorial/gitworkflow?view=vsts
  -

## Migrating to Git
