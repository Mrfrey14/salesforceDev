How to setup Jenkins from download to CI/CD:

1) Download the JDK if you haven't by going [here](https://www.oracle.com/java/technologies/javase-downloads.html)
2) Download the Jenkins Generic Java Package (.war file) from this [location](https://www.jenkins.io/download/) 
3) Open up a command line or powershell window, traverse to your downloads folder (cd downloads), and then run the following command: java -jar jenkins.war
4) After Jenkins installs successfully, grab the admin password in the command line window (it should display it). If you already closed it, no worries, open up your browser and type in localhost:8080 in the address bar. You should be presented with an "Unlock Jenkins" page and it will tell you where to go to get your password.
5) If you haven't already go to open up your browser and type in localhost:8080 in the address bar. You should be presented with a Jenkins login screen.
6) Enter the password it asks for and continue to the next page.
7) Unless you have a reason not to, click the "Install suggested Plugins" button to install Jenkins.
8) Create your admin user 