Sys.setenv(R_SERVR_PORT=5637)



# logo image

static/images/logo_1.png


# Merge statement
Step 1: From your project repository, bring in the changes and test.

git fetch origin
git checkout -b dev origin/dev
git merge master


Step 2: Merge the changes and update on GitHub.

git checkout master
git merge --squash  dev
git push origin master

Source: https://anotheruiguy.gitbooks.io/gitforeveryone/content/index.html
The merge
Getting your branched code merged into master is not a magical process, it's pretty simple really. What do we know? We know that we have a version of code on master and that we have more code in a brach called new-branch. It is the new code that we want merged into master. To get started, let's checkoutmaster`:

$ git checkout master
Ok, now we want to merge, but let's do a little check first. We can do a quick check to see what branches are merged and not merged into master

$ git branch --merged
At this point, we should only see the master branched listed. So then run this:

$ git branch --no-merged
This should return the new-branch in the list. Ok, let's merge these two. BUT, we need pass in the --no-ff flag. What does this do?

The --no-ff flag prevents git merge from executing a "fast-forward" if it detects that your current HEAD is an ancestor of the commit you're trying to merge. A fast-forward is when, instead of constructing a merge commit, git just moves your branch pointer to point at the incoming commit.

Occasionally you want to prevent this behavior from happening, typically because you want to maintain a specific branch topology (e.g. you're merging in a topic branch and you want to ensure it looks that way when reading history). In order to do that, you can pass the --no-ff flag and git merge will always construct a merge instead of fast-forwarding.

$ git merge new-branch --no-ff
Ok, but this may have just got weird and will freak you out.