### How to setup a project in VSCode for Salesforce projects whose source of truth is their Production Org

Note: Ctrl+Shift+P brings up the command palette in vscode. Remember it, you will constantly use it.

1) In the command palette run the SFDX: Create Project with Manifest command

        a) If you prefer the CLI you can run the sfdx force:project:create --projectname [name of your project] --manifest

2) When prompted choose the standard template (unless you have a reason not to), and enter a project name.

3) In the command palette run the SFDX: Authorize an Org command

        a) If you prefer CLI you can run the sfdx force:auth:web:login -a [alias name] -r [URL for your org]

4) When prompted, select the type of org you are connecting to, enter an alias (name to represent your org) and finally log in to your org when it pops up in the browser window.

5) You should see a "manifest" folder in your project. Inside that folder there should be a file called "package.xml". You can either leave it alone or update the package.xml file to include more metadata types to pull from your org. When you retrieve data in the next step, you will only retrieve data types declared in your package.xml file. For more information please check out the supplementary links section of this wiki article

6) In the command palette run the SFDX: Retrieve Source in Manifest from Org command. This should pull in all the metadata from your org that you outlined in your package.xml file.

         If you prefer CLI, run the following command: sfdx force:source:retrieve -x [path to your projects package.xml file]

7) In the command palette run the SFDX: Refresh SObject Definitions command so that you can get autocompletion on your object fields



***


### Supplementary links

[Link to package.xml examples](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/manifest_samples.htm)

[Link to Metadata Types you can add to package.xml file](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_types_list.htm)

           