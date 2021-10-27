git pull --rebase origin Localization

git reset --hard isaacdev

git fetch origin
git reset --hard origin/develop

git clean -f
git checkout -- *
git reset --hard


git rm --cached -r .
git reset --hard
