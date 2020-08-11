### How to setup local Git

***

For a lot of Salesforce projects there is no version control... and that just scares me. You can still protect yourself though with local git. This wiki will go over how to utilize local git while developing in IntelliJ/Illuminated Cloud.

1. First setup your Illuminated Cloud/Salesforce project in IntelliJ: (future link to IlluminatedCloud project setup wiki)

2. Go to VCS -> Enable Version Control Integration
    * For the question "Select a version control system to associate with the project root", select the option, "Git". Then click the "OK" button.

3. Go to File-> Preference ->Version Control -> Commit and check the box, "Use non-modal commit interface". Hit the "Apply" button and then the "Ok" button (This step is optional but I like this setup better personally).

4. You'll notice 3 things have now changed in your project.

    * All of your files are highlighted in red (this indicates the files are not currently added to your staging area and will not be commited)
    * On the left panel/bar underneath the "Structure" tab you will see a "Commit" tab. This is where you can see files that are "Unversioned" or not 
    added to your commit staging area as well as files that have changed that are in your currently checked out git branch.
    * On the bottom panel you will see a "Git" tab next to the "Log Analyzer" tab. This allows you to easily check out git branches, create new branches 
    and view file version history in the "Log" tab. It will also allow you to see the git console and run git commands via cli if you would rather use 
    the CLI commands. Currently all you will see in the "Log" tab is an empty master branch. Let's figure out how to add files to it.

5. In the "Commit" tab click the browse button next to the "Unversioned Files" checkbox. 

6. In the "Unversioned Files Modal" find the "src" folder and double click it. IntelliJ should now "Add" all of the files to the into the staging area for your currently checked out git branch (in our case the master branch).

7. In the "Commit" tab check the box next to the "Default Changelist", type in a meaningful commit message, and then press the "Commit" button in the bottom left corner.

* If you have the Code Analysis tool running for your commits a modal will pop-up informing you of code analysis problems. Press the "Commit" button to continue. These are not necessarily relevant until you configure the code analysis tool for your needs.
* If you have the, "TODO" reviewer active you may get another modal asking you if you would like to review your TODO's marked in your code, press the "Commit" button to continue. 
* If you want to edit what additional things run prior to committing a change, there is a gear icon to the right of the "Commit" button, press it to alter your pre-commit and post-commit settings.

8. The code will now be added to the master branch in the "Git" tab at the bottom of IntelliJ.

9. I personally suggest creating a branch after your first commit, committing new changes to that branch and then merging that branch with the master when you feel good about your new changes. I make at least one branch per day. 

* To create a branch, go to the "Git" tab, highlight the master branch and then hit the "+" button. Keep the "Checkout Branch" checkbox checked and name your branch something meaningful for what you're working on.
* Work on whatever code you need to work on, then, when you are done, go to the, "Commit" tab on the left side of IntelliJ, check the "Default Changelist" box (which will now only have files you have altered since your last commit) and commit those changes.
* After committing those changes to your branch, go to the "Git" tab on the bottom of IntelliJ, right click on the, "master" branch and click the "Checkout" option in the drop down list.
* Right click on your non-master branch and select the option, "Merge into current". This will merge your new branch into the master branch.
* After you merge the branch into the master branch you can right click it and delete it (this part is optional, but it helps keep things a bit cleaner day to day. Eventually your branches will add up). 

10. If at any time you want to see past versions (or your file history) for a file, click on the master branch, find the file, right click the file and choose the option, "History up to here". This will show you the many versions of your file.

_**For more information about using Git in IntelliJ. This is a very useful video:**_ [Using Git with IntelliJ Video Tutorial](https://www.youtube.com/watch?v=uUzRMOCBorg)

_**For more information about git in general and how it works, you can learn more here:**_ [Git beginner tutorial](https://www.youtube.com/watch?v=HVsySz-h9r4)
