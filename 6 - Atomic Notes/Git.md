
2026-02-20 21:59

Tags: [[obsidian_sync/3 - Tags/Git|Git]] 

# Git

## Initializing a git repo locally
to initialize a repo with the master branch named main
**git init -b main** 

Add all files and start tracking them
````
git add .
`````

If you want to ignore some files and not track them then 
````
touch .gitignore
`````

The add the file that you want to skip tracking in that text file.
Also if you want to stop tracking something that is already tracked do
````
git rm --cached FILENAME
`````
# References
