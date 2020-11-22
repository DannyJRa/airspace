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
git merge --squash --no-ff dev
git push origin master