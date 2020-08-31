### How to setup PMD for Apex in IntelliJ:


***


1. Download my pre-made Apex PMD Ruleset here (you can update this file to remove or add rules if you'd like to): [Apex PMD Ruleset](https://github.com/Coding-With-The-Force/SalesforceBestPractices/blob/master/apexRules.xml)

2. In IntelliJ go to File -> Setting -> Plugins. Then click the Marketplace Tab.

3. On the Marketplace tab type in "PMDPlugin" and install the PMDPlugin after it appears. After you have installed the PMDPlugin, restart IntelliJ.

4. After restarting IntelliJ go to File -> Settings -> PMD (The PMD tab in settings should be new unless PMDPlugin was already installed).

5. In the PMD area of Settings, make sure the "RuleSets" tab is selected. 

6. Press the + button to add a custom ruleset and then click the "Browse" button. After clicking the browse button find and select the Apex PMD Ruleset I provided to you in step 1 of this wiki.

7. After selecting the Apex PMD Ruleset hit the "OK" button to close the modal pop-up and then the "Apply" button in the Settings box.

8. Find a class in your project you would like to run PMD on and right click it. In the right-click menu you should see an option to "Run PMD" near the bottom. Hover over it and then hover over the "Custom Rules" area and select the Apex Rules you just added.

9. PMD should now run and inform you of any issues you have in your code.