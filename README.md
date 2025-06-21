# Hike Redux

You've just been on the worst hike of your life, but you're finally ready to
give it another shot. You join a hiking group and volunteer to use your new gear
to act as a scout. The group will slowly hike up the mountain while you branch
off to scout for shortcuts. When you find enough of them, rejoin the group and
share your new route with them. Keep climbing until you lead the group to the
peak!

## Instructions

1. Clone this repository to your computer and navigate to it using your terminal
2. Run `./new-game` in your terminal to begin the game.
3. Follow the on-screen instructions to complete the hike!

## Changing history with `git rebase`

Rebasing is a way to change your Git history. It's effectively saying, "pretend
I started this branch now instead of then." To rebase, run
`git rebase commit-goes-here` with the commit you wish you had branched from.
For example, if you have a `main` branch and a `feature` branch with these
commits:

```
                  o dddd  `feature`
                  |
`main`    zzzz o  o cccc
               | /
               |/
          bbbb o
               |
          aaaa o
```

Switching to the `feature` branch and running `git rebase zzzz` (or
`git rebase main`) would give you this commit history:

```
                  o dddd  `feature`
                  |
                  o cccc
                 /
                /
`main`    zzzz o
               |
          bbbb o
               |
          aaaa o
```

Note that since this command edits a branch's history, it will cause problems
for anyone that has the old version of the branch. That means it's usually only
appropriate to do on branches that aren't shared with anyone.

## Merging changes with `git merge`

To merge the changes from one branch into another, use `git merge`. If you've
rebased your changes first, the commits from the rebased branch will be added
right on top of the main branch. For example, if you have this history:

```
                  o dddd  `feature`
                  |
                  o cccc
                 /
                /
`main`    zzzz o
               |
          bbbb o
               |
          aaaa o
```

Running `git merge feature` from the `main` branch will result in this history:

```
`feature`, `main`  dddd o
                        |
                   cccc o
                        |
                   zzzz o
                        |
                   bbbb o
                        |
                   aaaa o
```

## Relevance

The most common use for rebasing is updating a feature branch with changes that
have been made since you created the branch. This allows you to stay up to date
with other people's changes before merging your changes into a main branch.

You can merge changes without rebasing, but the branch's history won't be linear
anymore:

```
`main`         o zzdd
               |\
               | \
               |  o dddd  `feature`
               |  |
               |  o cccc
               | /
               |/
          zzzz o
               |
          bbbb o
               |
          aaaa o
```

This makes some Git operations more complicated, such as visualizing your commit
history and searching through commits. Rebasing changes before merging is a best
practice.

Also note that if you have a lot of potentially conflicting changes with the
branching your rebasing from, it's a good idea to use techniques like
`git reset` to "squash" all of your commits into one big commit before rebasing.
Git attempts to reapply each commit one at a time during a rebase, and it's
possible to run into conflicts that are either resolved by later commits or will
need to keep being resolved repeatedly on each commit. Squashing makes it so
conflicts will occur once at most.
