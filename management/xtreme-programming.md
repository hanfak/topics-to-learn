# Xtreme Programming (XP)

## Pair Programming

- PingPong

## using git to set up paring

This Pill is also available as [a video](https://www.youtube.com/watch?v=sFAxF6QSPas).

## Scenario:

Ben, Roi, Ana and Irina are students and rotate pairs each day.  Each day they
want to choose one person’s Boris Bikes codebase as the base to work from.
However, they each want to keep progress from each day in their own
`boris-bikes` repo.  How
might they do this?

### Day One:
Pairs:  `[Ben, Roi], [Ana, Irina]`

Each person creates a `boris-bikes` repo on GitHub and clones onto their
machine.
Everyone creates a branch called `day-one`:
```
git checkout -b day-one
```

Ben adds Roi’s repo as a remote:
```
git remote add roi [uri to Roi’s repo]
```
Roi adds Ben’s repo as a remote:
```
git remote add ben [uri to Ben’s repo]
```
Ana and Irina do likewise.

When Roi finishes the first piece of code, he pushes to his own repo:
```
git push origin day-one
```
Ben then pulls Roi’s code:
```
git pull roi day-one
```
Ben makes some changes then pushes to his own repo:
```
git push origin day-one
```
Roi then pulls from Ben:
```
git pull ben day-one
```
Ana and Irina do likewise.

### Day Two:
Pairs: `[Ben, Ana], [Roi, Irina]`

Ben and Ana decide that Ana’s codebase is more advanced and that they will start
back from Ben’s and work forwards.
Firstly, they add each other as remotes.

Ben:
```
git remote add ana [uri to Ana’s repo]
```
Ana:
```
git remote add ben [uri  to Ben’s repo]
```

Ben is continuing from his existing codebase on `day-one` so creates a new
branch `day-two` (from `day-one`) and pushes it to his GitHub:
```
git checkout -b day-two
git push origin day-two
```
Ana, however, needs a branch with a completely new history to avoid merge
conflicts.  She creates an orphan branch and clears it:
```
git checkout —-orphan day-two
git reset —-hard
```
Ana then pulls Ben’s history into her `day-two` branch, so they are both in
sync:
```
git pull ben day-two
```
Irina and Roi do likewise.  Now the usual Git Pong process will work.  When Ben
finishes coding he pushes to his remote:
```
git push origin day-two
```
Ana pulls:
```
git pull ben day-two
```
And pushes when she has finished:
```
git push origin day-two
```
and Ben pulls:
```
git pull ana day-two
```
etc.  Roi and Irina do likewise.

### Day Three
Pairs: `[Ben, Irina], [Roi, Ana]`

Firstly, Roi and Ana add each other as remotes.

Roi:
```
git remote add ana [uri to Ana’s repo]
```
Ana:
```
git remote add roi [uri to Roi’s repo]
```
Roi and Ana decide to work from Ana’s repo.

Ana:
```
git checkout -b day-three
git push origin day-three
```
Roi:
```
git checkout —-orphan day-three
git reset —-hard
git pull ana day-three
```
and so it continues.
