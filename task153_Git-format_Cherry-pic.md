# Task 15.3 [git format-patch and cherry-pic]

## Objective<br>

Apply a specific commit from one branch to another

## Scenario<br>

```
  A---B---C devnet
 /         
D main
```

## End Goal<br>

```
  A---B---C devnet
 /         
D---B' main
```

## Instructions

1. Log into `https://gitlab.devnetexperttraining.com` and navigate to:<br>
   `Menu → Groups → Your groups → [your name] → Task 15.3`

2. Clone the repo into the folder `~/src/tasks`:

```bash
cd ~/src/tasks
git clone git@gitlab.devnetexperttraining.com:student-sushil-bhattacharjee-outlook-com/task-153.git
```

3. Create three new files in the **main** branch with the following:

| Filename     | File contents |
| ------------ | ------------- |
| task153a.txt | DevNet-main   |
| task153b.txt | DevNet-main   |
| task153c.txt | DevNet-main   |

4. Add and commit:

```bash
git add task153*.txt
git commit -m "D"
```

5. Create and switch to a new branch `certifications`:

```bash
git checkout -b certifications
```

6. Modify file contents and commit separately:

| Filename     | New content         | Commit message |
| ------------ | ------------------- | -------------- |
| task153a.txt | DevNet-Associate    | A              |
| task153b.txt | DevNet-Professional | B              |
| task153c.txt | DevNet-Expert       | C              |

7. Commit changes:

```bash
git add task153a.txt
git commit -m "A"
git add task153b.txt
git commit -m "B"
git add task153c.txt
git commit -m "C"
```

8. Create patch files for the last 3 commits:

```bash
git format-patch -3
```

> Generates: `0001-A.patch`, `0002-B.patch`, `0003-C.patch`

9. Review patch files to understand the diff/instructions Git will apply.

10. Switch to **main** branch and apply patch `B`:

```bash
git checkout main
git apply 0002-B.patch
```

11. Verify file contents:

* `task153a.txt`: unchanged
* `task153b.txt`: now contains `DevNet-Professional`
* `task153c.txt`: unchanged

12. Cherry-pick commit `C` directly:

```bash
git log certifications --oneline  # get hash of C
git cherry-pick <commit-hash>
```

Example:

```bash
git cherry-pick 7fc08b5312407d3430093d0d301ff945cbf1bbb3
```

13. Verify final file states:

* `task153a.txt`: `DevNet-main`
* `task153b.txt`: `DevNet-Professional`
* `task153c.txt`: `DevNet-Expert`

14. Push main branch to remote:

```bash
git push origin main
```

## References

* [git format-patch](https://git-scm.com/docs/git-format-patch)
* [git apply](https://git-scm.com/docs/git-apply)
* [git cherry-pick](https://git-scm.com/docs/git-cherry-pick)
