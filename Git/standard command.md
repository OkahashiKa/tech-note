# Git standard command

## create new branch

1. create new local branch.

    ``` bash
    git checkout -b [new_branch] origin/[new_branch]
    ```

2. create new lemote branch.

    ``` bash
    git push -u origin [new_branch]
    ```

   - With the [-u] option it will be set to tracking branch.

## show branch

``` bash
## show local branch only.
git branch

## show branch with lemote branch too.
git branch -a
```
