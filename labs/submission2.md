# 1.2:

1. All command outputs for object inspection.: 
- commit
```
git cat-file -p 08d3851
tree de914b4b2283bf5347f7f5b32c8009c0eb3df1d5
parent 9a01abcd8d3ec399cb0db5d38fce30408b719608
author fleeshka <chaikovskaya.ulyana@gmail.com> 1771148530 +0300
committer fleeshka <chaikovskaya.ulyana@gmail.com> 1771148530 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgujrrBf24qaqo3iTuauxWwmVU/r
 08NAjJ8hGJsihW/noAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQO4jDhX46NZtXpN57J5yrLd+TikkqI2b3PM5Y5I8w0jOZKQGg/TLZN15X9FeV1eJgt
 rG8dqy2O5PbYd9+a9ehQ4=
 -----END SSH SIGNATURE-----

Add test file
```
- tree
```
git cat-file -p de914b4b2283bf5347f7f5b32c8009c0eb3df1d5
040000 tree 2bcb538ae49751bc18a51a8373b883319008572b	.github
100644 blob 6e60bebec0724892a7c82c52183d0a7b467cb6bb	README.md
040000 tree a1061247fd38ef2a568735939f86af7b1000f83c	app
040000 tree a009361d37744f32572f5255e50bd5f701d1c701	labs
040000 tree d3fb3722b7a867a83efde73c57c49b5ab3e62c63	lectures
100644 blob 2eec599a1130d2ff231309bb776d1989b97c6ab2	test.txt
```
- blob
```
git cat-file -p 2eec599a1130d2ff231309bb776d1989b97c6ab2
Test content
```
2. Blob is an object that stores the exact contents of a file without any filename or directory information. Tree is an object that represents a directory, mapping filenames to blobs or other trees along with their permissions, thus defining the project’s structure at a specific snapshot. Commit is an object that points to a tree and records metadata such as parent commit(s), author, committer, message, and optional signature, forming a node in the repository’s history graph.
3. Git stores repository data as a content-addressable object database, where every file snapshot, directory structure, and commit is saved as a compressed object identified by a cryptographic hash of its contents. This design enables immutability, efficient deduplication of identical data, and the construction of history as a chain of commits that reference trees and parent commits rather than storing full copies of the project each time.
4. 
- blob content (test.txt):
```
git cat-file -p 2eec599a1130d2ff231309bb776d1989b97c6ab2
Test content
```
- tree content (.github):
```
git cat-file -p 2bcb538ae49751bc18a51a8373b883319008572b
100644 blob 6f4f85c2442956ce747ef407b3d63766199b059c	pull_request_template.md
```
- commit content (same as first code snapshot from task 1):
```
git cat-file -p 08d3851
tree de914b4b2283bf5347f7f5b32c8009c0eb3df1d5
parent 9a01abcd8d3ec399cb0db5d38fce30408b719608
author fleeshka <chaikovskaya.ulyana@gmail.com> 1771148530 +0300
committer fleeshka <chaikovskaya.ulyana@gmail.com> 1771148530 +0300
gpgsig -----BEGIN SSH SIGNATURE-----
 U1NIU0lHAAAAAQAAADMAAAALc3NoLWVkMjU1MTkAAAAgujrrBf24qaqo3iTuauxWwmVU/r
 08NAjJ8hGJsihW/noAAAADZ2l0AAAAAAAAAAZzaGE1MTIAAABTAAAAC3NzaC1lZDI1NTE5
 AAAAQO4jDhX46NZtXpN57J5yrLd+TikkqI2b3PM5Y5I8w0jOZKQGg/TLZN15X9FeV1eJgt
 rG8dqy2O5PbYd9+a9ehQ4=
 -----END SSH SIGNATURE-----

Add test file
```

# 2.2:

1.
```
git switch -c git-reset-practice
Switched to a new branch 'git-reset-practice'

echo "First commit" > file.txt && git add file.txt && git commit -m "First commit"
[git-reset-practice 3ab8bfa] First commit
 1 file changed, 1 insertion(+)
 create mode 100644 file.txt

echo "Second commit" >> file.txt && git add file.txt && git commit -m "Second commit"
[git-reset-practice 492e2b3] Second commit
 1 file changed, 1 insertion(+)

echo "Third commit"  >> file.txt && git add file.txt && git commit -m "Third commit"
[git-reset-practice 85b268c] Third commit
 1 file changed, 1 insertion(+)

git reset --soft HEAD~1

git reset --hard HEAD~1
HEAD is now at 3ab8bfa First commit

git reflog
3ab8bfa (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to HEAD~1
492e2b3 HEAD@{1}: reset: moving to HEAD~1
85b268c HEAD@{2}: commit: Third commit
492e2b3 HEAD@{3}: commit: Second commit
3ab8bfa (HEAD -> git-reset-practice) HEAD@{4}: commit: First commit
08d3851 (main) HEAD@{5}: checkout: moving from main to git-reset-practice
08d3851 (main) HEAD@{6}: commit: Add test file
9a01abc (origin/main, origin/HEAD) HEAD@{7}: clone: from github.com:fleeshka/DevOps-Intro.git

git reset --hard 85b268c
HEAD is now at 85b268c Third commit
```

I created a separate branch to safely experiment with history rewriting, then made three sequential commits to generate a clear commit chain for testing.

I ran git reset --soft HEAD~1 to move the branch pointer back one commit while keeping changes staged, and then git reset --hard HEAD~1 to move back again while discarding both the index and working directory changes.

Finally, I used git reflog to locate the previous commit state and git reset --hard 85b268c to restore the branch to the lost “Third commit,” demonstrating how reflog enables recovery after destructive resets.

2.
```
git log --oneline
85b268c (HEAD -> git-reset-practice) Third commit
492e2b3 Second commit
3ab8bfa First commit
08d3851 (main) Add test file
9a01abc (origin/main, origin/HEAD) Merge pull request #1 from fleeshka/feature/lab1
47dfc6f docs: add lab1 submission stub
9a18fea docs: add commit signing summary
f2ef5b1 docs: add commit signing summary
d6b6a03 Update lab2
87810a0 feat: remove old Exam Exemption Policy
1e1c32b feat: update structure
6c27ee7 feat: publish lecs 9 & 10
1826c36 feat: update lab7
3049f08 feat: publish lec8
da8f635 feat: introduce all labs and revised structure
04b174e feat: publish lab and lec #5
67f12f1 feat: publish labs 4&5, revise others
82d1989 feat: publish lab3 and lec3
3f80c83 feat: publish lec2
499f2ba feat: publish lab2
af0da89 feat: update lab1
74a8c27 Publish lab1
f0485c0 Publish lec1
31dd11b Publish README.md
```
```
git reflog
85b268c (HEAD -> git-reset-practice) HEAD@{0}: reset: moving to 85b268c
3ab8bfa HEAD@{1}: reset: moving to HEAD~1
492e2b3 HEAD@{2}: reset: moving to HEAD~1
85b268c (HEAD -> git-reset-practice) HEAD@{3}: commit: Third commit
492e2b3 HEAD@{4}: commit: Second commit
3ab8bfa HEAD@{5}: commit: First commit
08d3851 (main) HEAD@{6}: checkout: moving from main to git-reset-practice
08d3851 (main) HEAD@{7}: commit: Add test file
9a01abc (origin/main, origin/HEAD) HEAD@{8}: clone: from github.com:fleeshka/DevOps-Intro.git
```

3. 
- git reset --soft HEAD~1 moved the branch pointer back one commit in history while leaving both the index (staging area) and working tree unchanged, so the reverted commit’s changes remained staged.
- git reset --hard HEAD~1 then moved history back again and forcibly aligned both the index and working tree to that earlier commit, discarding any staged or working directory changes introduced by the removed commits.

4. The recovery worked because git reflog records every movement of HEAD, including resets that rewrite branch history, even when commits become unreachable from the current branch tip. After the --soft and --hard resets moved the branch from the Third commit to the First commit, the Third commit (85b268c) was no longer visible in normal git log, but it still appeared in the reflog as HEAD@{2}. By identifying that hash in the reflog and running git reset --hard 85b268c, the branch pointer, index, and working tree were all restored to the exact state of the lost commit, effectively undoing the destructive reset.

# 3:

1, 2.
```
git log --oneline --graph --all
* 54279f3 (side-branch) Side branch commit
* 85b268c (HEAD -> git-reset-practice) Third commit
* 492e2b3 Second commit
* 3ab8bfa First commit
* 08d3851 (main) Add test file
*   9a01abc (origin/main, origin/HEAD) Merge pull request #1 from fleeshka/feature/lab1
|\  
| | * 4b587d9 (origin/feature/lab1) docs: update submission, finalize
| | * add170f docs: add lab1 submission stub
| |/  
| * 47dfc6f docs: add lab1 submission stub
|/  
* 9a18fea docs: add commit signing summary
* f2ef5b1 docs: add commit signing summary
* d6b6a03 Update lab2
* 87810a0 feat: remove old Exam Exemption Policy
* 1e1c32b feat: update structure
* 6c27ee7 feat: publish lecs 9 & 10
* 1826c36 feat: update lab7
* 3049f08 feat: publish lec8
* da8f635 feat: introduce all labs and revised structure
* 04b174e feat: publish lab and lec #5
* 67f12f1 feat: publish labs 4&5, revise others
* 82d1989 feat: publish lab3 and lec3
* 3f80c83 feat: publish lec2
* 499f2ba feat: publish lab2
* af0da89 feat: update lab1
* 74a8c27 Publish lab1
* f0485c0 Publish lec1
* 31dd11b Publish README.md
```

3. Graph view makes the commit structure visually explicit, clearly showing where branches diverge, merge, and how git-reset-practice, side-branch, and main relate to each other. Seeing history as a graph rather than a linear list makes it much easier to understand how resets move branch pointers and how commits remain in the repository even when they are no longer at the tip of a branch.

# 4:

1. 
```
git tag v1.0.0

git push origin v1.0.0
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 16 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (12/12), 1.38 KiB | 706.00 KiB/s, done.
Total 12 (delta 7), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (7/7), completed with 1 local object.
To github.com:fleeshka/DevOps-Intro.git
 * [new tag]         v1.0.0 -> v1.0.0

echo "temp" >> file.txt && git add file.txt && git commit -m "for v1.1.0"
[git-reset-practice 697f986] for v1.1.0
 1 file changed, 1 insertion(+)

git tag v1.1.0

git push origin v1.1.0
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 524 bytes | 524.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:fleeshka/DevOps-Intro.git
 * [new tag]         v1.1.0 -> v1.1.0
```
2.
85b268c0b137b8b066cf747d045311e1b3db049d
697f986e8bf3203e50b0f0a2208494dab41e800f

3.
Git tags are essential for marking specific points in your repository's history as important releases, enabling clear versioning that makes it easy to identify and rollback to stable versions. In CI/CD pipelines, tags often trigger automated deployment processes, and they serve as anchor points for generating release notes by comparing changes between tagged versions.

# 5:

1. 
```
git switch -c cmd-compare
Switched to a new branch 'cmd-compare'

git switch -
Switched to branch 'git-reset-practice'

echo "scratch" >> demo.txt
git add demo.txt
git restore demo.txt
git restore --staged demo.txt
```

2.
```
git status
On branch git-reset-practice
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	**Deliverable:**
	demo.txt
	labs/submission2.md
	witch -c cmd-compare

nothing added to commit but untracked files present (use "git add" to track)

git branch
  cmd-compare
* git-reset-practice
  main
  side-branch
```

3. 
- git restore demo.txt is used when you want to permanently discard all uncommitted changes in your working directory and revert the file back to its last committed state.
- git restore --staged demo.txt is used when you want to remove a file from the staging area while preserving all your local changes in the working directory.
- git restore --source=HEAD~1 demo.txt is used when you need to revert a file to exactly how it appeared in a previous commit, whether to undo unwanted changes or recover a deleted file.

# 6:

all done

# GitHub Community
Starring repositories matters in open source because it serves as both a personal bookmarking system for interesting projects and a public signal of appreciation that helps projects gain visibility, attract contributors, and build community trust through higher star counts. Following developers is essential in team projects and professional growth as it enables you to learn from experienced developers' code, discover new tools and trends, build valuable professional connections, and demonstrate your engagement with the developer community to potential employers.
