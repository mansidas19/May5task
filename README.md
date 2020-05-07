This project consists of four parts:
1.developer team 
2.SCM
3.Quality assurance team 
4.operatios team 

I am using Jenkins to integrate developer part which is in my bare metal os windows 10 with redhat linux 8 which is my guest os containing quality assurance team and operations part launched in docker container


First of all in the developer team,the developer will create the code.
I created a repository in github named "May5task".In git bash in the command line I used git clone command to clone the repository. 
Inside "May5task" I made a branch "dev1".
I made a git hook in .git/hooks/post-commit that will automatically push the changes made in both the branches master as well as dev1 once they are committed.


In the SCM part the github maintains all the different versions of our code.


Inside jenkins I am giving three jobs.
1.project job1.1- this job will keep track of dev1 branch in github every minute using pollscm and will download the code in its workspace whenever there is any changes. Then it will further copy the code to "testing" folder created in redhat linux 8.
  project job1.2- this job will launch a new docker container of httpd image(if it doesn't exist) and mount "testing" folder with /usr/local/apache2/htdocs folder where all the code will be copied and hosted in webserver. 
2.project job 2.1- similarly this job will keep track of master branch and download and copy the code in "may5" folder in redhat linux 8whenever there will be any changes. 
  project job 2.2- this job will launch a new docker container of httpd image and copy code of "may5" folder to /usr/local/apache2/htdocs folder which will host webserver publicly as we allow PAT here.
3- job3 - when the quality assurance team will give green signal that job1.1 and 1.2 are running absolutely fine this job will merge the two branches and ultimately host it in public webserver. 
