FIRST OF ALL I WOULD THANK MR.VIMAL DAGA SIR FOR TEACHING A LOT OF THINGS WITH ALL ITS BASIC CONCEPTS AND DEVELOPING YOUNG MINDS IN SUCH A SHORT PERIOD OF TIME.

THIS PROJECT CONTAINS FOUR PARTS-
1.DEVELOPER 
2.SCM
3.TESTING
4.OPERATIONS

WE ARE USING JENKINS TO INTEGRATE ALL OF THEM TOGETHER.

We are creating a repository "May5task" in github.
In git bash command line I am cloning this repository,creating new branch, making changes in index.html file in both master and dev1 branch and pushing it to github using git hooks automatically after commit.
In jenkins I am building one job for dev1 branch and one for master branch.


For dev1 branch following 2 jobs:
1.project job1.1 - this will keep check on github repo dev1 branch every minute using pollscm and download the code in workspace whenever there are any changes and copy to "testing" folder created in redhat linux 8(base os) from where jenkins is launched.
2.project job1.2 - this will create docker container of httpd image and copy contents of "testing" folder in /usr/local/apache2/httpd folder and run in base os browser only if there is no error in code (basically in testing part) and will build only if the "project job1.1" is successfully build. 
3.job3 - if the above 2 jobs are successfully build this will copy the code from dev1 branch and update in "may5" folder and will further launch docker container of httpd image and copy contents of "may5" folder in /usr/local/apache2/httpd folder and run in base os browser as well as outside world as we enable PAT here only if there is no error in code.


# git clone "URL OF GITHUB REPO"
# cd May5task
# git branch dev1
# cat >index.html
hi
# git add index.html
# git .git/hooks/post-commit
#!/bin/bash
git push
# git commit index.html -m first


