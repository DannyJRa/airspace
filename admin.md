Sys.setenv(R_SERVR_PORT=5637)



ou should be able to use the "ours" merge strategy to overwrite master with seotweaks like this:

Aus <https://stackoverflow.com/questions/2862590/how-to-replace-master-branch-in-git-entirely-from-another-branch> 


git checkout seotweaks
git merge -s ours master
git checkout master
git merge seotweaks

Aus <https://stackoverflow.com/questions/2862590/how-to-replace-master-branch-in-git-entirely-from-another-branch> 

test