# Git Adventure Game Guide

This guide walks the player through [Bloomberg's Git adventure game](https://github.com/bloomberg/git-adventure-game). As the game encourages learning through experimentation and exploration, this document serves as a reminder for what I've discovered along this journey.

> This is a living document. Updates will come through repeated plays as I learn more about Git.

## Table of contents

- [Git Adventure Game Guide](#git-adventure-game-guide)
  - [Table of contents](#table-of-contents)
  - [Concepts](#concepts)
    - [HEAD](#head)
  - [Walkthrough](#walkthrough)
    - [Commit changes](#commit-changes)
    - [Switch branches](#switch-branches)
    - [Show commit logs](#show-commit-logs)
    - [Combine other commits into the current branch](#combine-other-commits-into-the-current-branch)
    - [Show the last change made to each line of a file](#show-the-last-change-made-to-each-line-of-a-file)
    - [Restore a file to a previous commit](#restore-a-file-to-a-previous-commit)
    - [Manage tracked repositories](#manage-tracked-repositories)
    - [Move or combine commits to a new base commit](#move-or-combine-commits-to-a-new-base-commit)
    - [Search for text in a file's history](#search-for-text-in-a-files-history)
    - [Define shortcuts](#define-shortcuts)
    - [Apply changes introduced by some existing commits](#apply-changes-introduced-by-some-existing-commits)
  - [Things not covered that every beginner wants to know](#things-not-covered-that-every-beginner-wants-to-know)
    - [Undo one or more commits](#undo-one-or-more-commits)

## Concepts

### HEAD

`HEAD` or `HEAD~0` is a pointer to the latest commit in a branch. `HEAD^` or `HEAD~1` is a pointer to the second latest commit in a branch, `HEAD~2` is a pointer to the third latest, and so on. Use these to step back in time through previous commits without need to know the commit object names.

([Back to top](#table-of-contents))

## Walkthrough

### Commit changes

The game begins with you committing to changes you've made in your version of a repository. After making the **talisman**, commit your changes with the following:

```bash
# Show all changes that haven't been committed.
git status

# Add all new and edited files to be committed.
git add .

# Commit the changes with a useful message.
git commit -m "<message>"
```

([Back to top](#table-of-contents))

### Switch branches

To proceed to Level 1, you're told how to switch branches like so:

```bash
# List existing branches.
git branch

# Switch to an existing branch.
git checkout <branch>
```

([Back to top](#table-of-contents))

### Show commit logs

Level 1 ( `git checkout 01_the_walls_have_ears` ) introduces commit logs that review past changes to the repository. The following command will print past commit messages in reverse chronological order.

```bash
git log
```

Reviewing the logs will get you your answer. Don't forget to [commit your changes](#commit-changes) after making the **talisman**.

([Back to top](#table-of-contents))

### Combine other commits into the current branch

In Level 2 ( `git checkout 02_whimsical_elf` ), you learn to merge changes from two or more commits into the current branch, handling any conflicts you encounter.

```bash
# The commit here is usually the HEAD of the other branch, so it's possible to
# replace the commit with the branch name, i.e., git merge <branch>
git merge <commit>
```

> Remember, you can use `git branch` to list existing branches to merge with.

If there are no conflicts among the commits, the merge will succeed. Otherwise, you might get the following message:

```
Auto-merging <filename>
CONFLICT (content): Merge conflict in <filename>
Automatic merge failed; fix conflicts and then commit the result.
```

`git status` will notify you of unmerged paths and provide the steps to resolve them. To fix conflicts, open the modified file and resolve the changes manually. It will look something like this:

```
<<<<<<< Current branch
Segment conflicting with the other branch
=======
Segment conflicting with the current branch
>>>>>>> Other branch
```

Simply keep the segments you want or remove them otherwise. Segments are marked with `<<<<<<<`, `=======` and `>>>>>>>` to show which segments belong to which branch. Don't forget to remove the markers when you're done. Then proceed to [commit the changes](#commit-changes).

([Back to top](#table-of-contents))

### Show the last change made to each line of a file

Level 3 ( `git checkout 03_goblin_treasury` ) lets you do some detective work with Git. Sometimes, you want to find out who committed the last "offence" to a specific line of a file so you know who to point fingers at. This is aptly done with:

```bash
git blame <filename>
```

Write the offender's name on the **talisman** to continue.

([Back to top](#table-of-contents))

### Restore a file to a previous commit

Level 4 ( `git checkout 04_lewis_carroll` ) teaches you how to travel back in time to undo your most recent mistakes.

```bash
# View a file's contents from a previous commit.
git show <commit>:<filename> | less

# View a file's contents from a number of commits ago.
git show HEAD~<number>:<filename> | less

# Overwrite a file with that from a previous commit.
git show <commit>:<filename> > <filename>
```

([Back to top](#table-of-contents))

### Manage tracked repositories

Level 5 ( `git checkout 05_desert` ) introduces the concept of *remotes*, i.e., remote connections to repositories. Think of them as portals to parallel universes. They allow access to files in other repositories.

```bash
# List available remotes.
git remote

# Add and <name> a remote from <url>.
git remote <name> <url>

# Download objects and references from the remote <name>.
git fetch <name>

# Remove the remote <name> and all its objects and references.
git remote remove <name>
```

You can now [merge](#combine-other-commits-into-the-current-branch) the **rain_clouds** from the remote to the current branch.

([Back to top](#table-of-contents))

### Move or combine commits to a new base commit

Level 6 ( `git checkout 06_magic_potion` ) mixes things up by — quite literally — letting you mix up past commits without creating merge commits. It requires these commits to belong to the same branch.

```bash
# Edit the list of commits using the default editor before rebasing.
git rebase -i <base>

# git rebase only looks at commit names and not messages.
# "pick" keeps a commit. You can reorder lines to reorder commits.
# "edit" lets you edit the files and/or the commit message.
# "reword" lets you edit just the commit message.
# "drop" deletes the commit. Removing the line works too.
# "squash" or "fixup" after "pick" folds subsequent commits into the first.
```

To complete the level, swap lines 6 and 7, then delete line 4 in the editor.

([Back to top](#table-of-contents))

### Search for text in a file's history

Level 7 ( `git checkout 07_look_into_the_past` ) encourages you to fish for words in a file's history currently missing in that file.

```bash
# List all commit objects of a file in reverse chronological order.
git rev-list --all -- <filename>

# List all lines in a file's commit history containing <text>.
git grep <text> $(git rev-list --all -- <filename>) -- <filename>
```

Write the name in the **talisman** to continue.

([Back to top](#table-of-contents))

### Define shortcuts

Level 8 ( `git checkout 08_mystical_creatures` ) is about shortcuts! Enough said.

```bash
# Add a single file to be committed.
git add <filename>

# Define an alias for <a_very_long_git_command>.
# Then "git <a_very_long_git_command>" can be shortened to "git <alias>".
git config alias.<alias> '<a_very_long_git_command>'
```

([Back to top](#table-of-contents))

### Apply changes introduced by some existing commits

Level 9 ( `git checkout 09_mystical_creatures` ) ends the adventure with some nifty commands you wished you had access to from the start:

```bash
# "--oneline" combines "--pretty=oneline" and "--abbrev-commit".
# "--pretty=oneline" pretty-prints the commit logs in single lines.
# "--abbrev-commit" shortens the commit object name to a unique prefix.
# "--graph" draws an ascii graph of the commit history on the left.
git log --oneline --all --graph -- <filename>

# Apply existing commits (from other branches) and record a new commit each.
# Conflicting paths will require merging.
git cherry-pick <commit>
```

Writing the revealed name on a **talisman** completes the adventure.

([Back to top](#table-of-contents))

## Things not covered that every beginner wants to know

### Undo one or more commits

```bash
# Undo the last commit and staging.
git reset HEAD~

# Undo the last commit but keep changes in staging.
git reset --soft HEAD~

# Commit new changes using the old commit message.
git commit -c ORIG_HEAD

# Discard all changes after <commit>. DANGEROUS! USE WITH CARE!
git reset --hard <commit>
```

([Back to top](#table-of-contents))
