### How to setup a project in VSCode for Salesforce projects whose source of truth is their Production Org

_Note: Ctrl+Shift+P brings up the command palette in vscode. Remember it, you will constantly use it._


***

**How to setup a project and connect your org**

1) In the command palette run the SFDX: Create Project with Manifest command

        a) If you prefer the CLI you can run the sfdx force:project:create --projectname [name of your project] --manifest

2) When prompted choose the standard template (unless you have a reason not to), and enter a project name.

3) In the command palette run the SFDX: Authorize an Org command

        a) If you prefer CLI you can run the sfdx force:auth:web:login -a [alias name] -r [URL for your org]

4) When prompted, select the type of org you are connecting to, enter an alias (name to represent your org) and finally log in to your org when it pops up in the browser window.

***

**How to retrieve data from your org using the [Org Browser](https://developer.salesforce.com/tools/vscode/en/user-guide/org-browser) (New way)**

1) After connecting your org using the steps outlines above, click the cloud icon on the left side of the VSCode window. Clicking it should display a list of all the metadata types available to pull in your org.

2) If you hover over a metadata type you will see a button to the right of it that looks like a cloud with an arrow in the center of it. Clicking this button will retrieve the metadata type from your org and place it in your project.

***

**How to retrieve data from your org using the [manifest package.xml file](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/manifest_samples.htm) (Old way)**

1) You should see a "manifest" folder in your project. Inside that folder there should be a file called "package.xml". You can either leave it alone or update the package.xml file to include more metadata types to pull from your org. When you retrieve data in the next step, you will only retrieve data types declared in your package.xml file. For more information please check out the supplementary links section of this wiki article

2) In the command palette run the SFDX: Retrieve Source in Manifest from Org command. This should pull in all the metadata from your org that you outlined in your package.xml file.

         If you prefer CLI, run the following command: sfdx force:source:retrieve -x [path to your projects package.xml file]


***

**How to get auto-complete to work for object fields in your org**

1) In the command palette run the SFDX: Refresh SObject Definitions command so that you can get autocompletion on your object fields


***

**How to Auto-Deploy to your org on Save (Ctrl+S)**

1) In VSCode go to File -> Preferences -> Settings. 

2) Click the Extensions drop down

3) Click the Salesforce Feature Previews extension

4) Check the box next to "Push-or-deploy-on-save"


***

**Other Useful Features To Enable**

1) In the extension settings under "Salesforce Apex Configuration" there is a checkbox for "Enable-sobject-refresh-on-startup". This automatically refreshes your sobjects from your org when your project is loaded.

2) In the extension settings under "Salesforce Feature Previews" there is a checkbox for "Detect Conflicts At Sync". This enables conflict detection when deploying a save to your orgs. It can help to prevent overwriting data.

***


### Supplementary links

[Link to package.xml examples](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/manifest_samples.htm)

[Link to Metadata Types you can add to package.xml file](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_types_list.htm)

[Org Browser Documentation](https://developer.salesforce.com/tools/vscode/en/user-guide/org-browser)

[Org Development Model Setup](https://developer.salesforce.com/tools/vscode/en/user-guide/development-models)       

[SF VSCode Plugins Documentation](https://developer.salesforce.com/tools/vscode/en/getting-started/install) 

[SFDX CLI Project Commands](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_project.htm#cli_reference_force_project_create)

[SFDX CLI Login Commands](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_auth.htm#cli_reference_force_auth_web_login) 

[SFDX CLI Source Commands](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_source.htm#cli_reference_force_source_retrieve)  