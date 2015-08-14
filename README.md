## Slides on fuzzing and Mozilla in 2015
#### ... and where fuzzing sits in a Mozilla workflow.



---

###### To obtain slide template:

```
# Change the following variables as desired.
TREES_LOCATION=~/trees/
NEW_REPO_NAME=2015-fuzzing-and-mozilla
REMOTE_REPO_LOCATION=git@github.com:nth10sd/mozilla-presentation-templates.git
FILES_TO_BE_IGNORED="*.key *.zip README.md html5/pictures/* html5/firefox-os-pick-and-mix* html5/mozilla-mission.html"
TEMP_REPO_NAME=tmpRepo

# Clone to temporary repository.
git clone $REMOTE_REPO_LOCATION $TREES_LOCATION/$TEMP_REPO_NAME
cd $TREES_LOCATION/$TEMP_REPO_NAME

# Prune unneeded files that are not part of the HTML5 template, as well as media files from the template.
# Adapted from http://stackoverflow.com/a/3910697/445241
git filter-branch --prune-empty --index-filter "git rm --cached --ignore-unmatch $FILES_TO_BE_IGNORED" HEAD
git clone $TREES_LOCATION/$TEMP_REPO_NAME $TREES_LOCATION/$NEW_REPO_NAME
cd $TREES_LOCATION/$NEW_REPO_NAME/

# Make .git smaller, from http://stackoverflow.com/a/17864475/445241
rm -rf .git/refs/original/ && git reflog expire --all && git gc --aggressive --prune=now
git reflog expire --all --expire-unreachable=0
git repack -A -d
git prune

# We should have a smaller .git, without unwanted files.
du -h .git

# Remove temporary repository.
rm -rf $TREES_LOCATION/$TEMP_REPO_NAME

# Move from html5 subdirectory to the main directory. You will have to commit this change later.
git mv html5/* .
rmdir html5

ls

```
