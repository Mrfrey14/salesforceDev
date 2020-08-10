### How to setup local Git

***

For a lot of Salesforce projects there is no version control... and that just scares me. You can still protect yourself though with local git. This wiki will go over how to utilize local git while developing in IntelliJ/Illuminated Cloud.

1. First setup your Illuminated Cloud/Salesforce project in IntelliJ: (future link to IlluminatedCloud project setup wiki)

2. Go to VCS -> Enable Version Control Integration
    * For the question "Select a version control system to associate with the project root", select the option, "Git". Then click the "OK" button.

3. You'll notice 3 things have now changed in your project.

    * All of your files are highlighted in red (this indicates the files are not currently added to your staging area and will not be commited)
    * On the left panel/bar underneath the "Structure" tab you will see a "Commit" tab. This is where you can see files that are "Unversioned" or not 
    added to your commit staging area as well as files that have changed that are in your currently checked out git branch.
    * On the bottom panel you will see a "Git" tab next to the "Log Analyzer" tab. This allows you to easily check out git branches, create new branches 
    and view file version history in the "Log" tab. It will also allow you to see the git console and run git commands via cli if you would rather use 
    the CLI commands. Currently all you will see in the "Log" tab is an empty master branch. Let's figure out how to add files to it.

4. In the "Commit" tab click the browse button next to the "Unversioned Files" checkbox. 
5. In the "Unversioned Files Modal" find the "src" folder and double click it. IntelliJ should now "Add" all of the files to the into the staging area for your currently checked out git branch (in our case the master branch).
6. In the "Commit" 