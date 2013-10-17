Change detection script based on git

Dependancy : you should have git installed 

I. Preparation
 
0) Choose the directories you want to track

1) Enter the first directory you want to track
	cd /local

2) Initialize the git repo and add everything under this directory
	git init ; git add .

3) Look for files that should be ignored by git :
   file that are changing often and/or automaticaly like logs, generated
   datas etc.  Wait a few minutes, then do :

	git status -s | grep '^.[^ ]'

        AM var/log/auth.log

  You want to ignore the files that recently changed.

  Add the modified files to to .gitignore
  Preferably add the parent directory if there are many files :

	vi .gitignore

	var/log

4) once .gitignore has a few list of files, remove the
  .git directory and start again
	rm -fr .git
	git init ; git add .
	etc.

5) do that until you find no more files to ignore,
   you can do the initial commit

6) Repeat step 1 to 5 for each tracked directory in the list

II. Setup

1) Install the script 
	sh ./INSTALL

2) Configure the directory list
	vi /local/etc/changedetection.conf

	# add each directory sepated by a newline
	/etc
	/local

3) Add a cron entry

PATH=/etc:/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin
#
MAILTO = syadmins@example.com
1-59/1  *       *       *       *       root /local/bin/keepstate changedetection.state /local/bin/changedetection
