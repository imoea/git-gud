# Git Gud Guides

This list of guides will help you get good with Git.

- [Git Adventure Game](git-adventure-game.md)
- [Oh My Git!](https://blinry.itch.io/oh-my-git) [TODO]

## Table of contents

- [Git Gud Guides](#git-gud-guides)
  - [Table of contents](#table-of-contents)
  - [Things every beginner wants to know](#things-every-beginner-wants-to-know)
    - [Undo one or more commits](#undo-one-or-more-commits)

## Things every beginner wants to know

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
