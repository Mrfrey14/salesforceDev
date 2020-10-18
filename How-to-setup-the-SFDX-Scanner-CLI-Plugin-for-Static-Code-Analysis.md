### How to setup the SFDX Scanner CLI Plugin for Static Code Analysis

1) Install the [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/javase-downloads.html) version 8 or higher

2) Install the [Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli)

3) Install the sfdx scanner plugin for the Salesforce CLI by opening up a terminal window and running the following command `sfdx plugins:install @salesforce/sfdx-scanner`

4) Create a [Salesforce Project in VSCode](https://github.com/Coding-With-The-Force/SalesforceBestPractices/wiki/How-to-Setup-a-Salesforce-VSCode-Project-(Org-Development-Model))

5) Open the Terminal in VSCode and run the following command to scan your entire codebase for all static code issues: `sfdx scanner:run --target "**/default/**" --format "csv" --outfile "pathToFile.csv" (make sure to replace pathToFile.csv with the actual path for your file)

6) The above command will output a csv that shows you all of the issues with the code in your org within a few seconds (unless you have a mega code-base. It may take a few minutes then).

7) For more information on the wealth of configuration options you have with this cli plugin, please check out the supplementary info links.

***
Supplementary Info

[SFDX Scanner Github Repo](https://github.com/forcedotcom/sfdx-scanner)

[SFDX Scanner Documentation](https://forcedotcom.github.io/sfdx-scanner/)