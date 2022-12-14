### How to setup a project in VSCode for Salesforce projects whose source of truth is their Production Org

_Note: Ctrl+Shift+P brings up the command palette in vscode. Remember it, you will constantly use it._


***

**Things you need to install**

1) Install [VSCode](https://code.visualstudio.com/download)

2) Install the [Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli)

3) Install the [Salesforce VSCode Extension Pack](https://marketplace.visualstudio.com/items?itemName=salesforce.salesforcedx-vscode) in VSCode

4) This download step is optional, but Node.js will come in handy eventually: [Install node.js and npm](https://nodejs.org/en/download/)
***


**How to setup a project and connect your org**

1) In the command palette run the SFDX: Create Project with Manifest command

        a) If you prefer the CLI you can run the sfdx force:project:create --projectname [name of your project] --manifest

2) When prompted choose the standard template (unless you have a reason not to), and enter a project name.

3) In the command palette run the SFDX: Authorize an Org command

        a) If you prefer CLI you can run the sfdx force:auth:web:login -a [alias name] -r [URL for your org]

4) When prompted, select the type of org you are connecting to, enter an alias (name to represent your org) and finally log in to your org when it pops up in the browser window.

***

**How to retrieve data from your org using the [Org Browser](https://developer.salesforce.com/tools/vscode/en/user-guide/org-browser)**

1) After connecting your org using the steps outlines above, click the cloud icon on the left side of the VSCode window. Clicking it should display a list of all the metadata types available to pull in your org.

2) If you hover over a metadata type you will see a button to the right of it that looks like a cloud with an arrow in the center of it. Clicking this button will retrieve the metadata type from your org and place it in your project.

***

**How to retrieve data from your org using the [manifest package.xml file](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/manifest_samples.htm)**

_**Note:**_ There is a VSCode extension to simplify setting up your package.xml manifest files called [Salesforce Package.xml Generator](https://marketplace.visualstudio.com/items?itemName=VignaeshRamA.sfdx-package-xml-generator). It will make your life way easier.

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

**How to do Execute Anonymous in VSCode**

1) Locate the top level folder "scripts", then open its subfolder "apex"

2) Create a new apex file in the "apex" folder and write your code in that file.

3)  In the command palette run the SFDX: Execute Anonymous Apex With Editor Contents command


***

**How to do SOQL queries in VSCode**

1) In the command palette run the SFDX: Execute SOQL Query command

2) Choose whether it's a REST API or Tooling API Query (Most queries will use the REST API)

3) Type your query and hit enter


***

**Useful VSCode and SFDX CLI Plugins for Salesforce Development**

1) [Salesforce Scanner CLI Plugin](https://forcedotcom.github.io/sfdx-scanner/en/scanner-commands/run/) - This plugin allows you to run PMD, ESLint and security scans on your code and output them to files in various formats. It's the most comprehensive code scanner to date that's completely free.

2) [Salesforce LWC Dev Server CLI Plugin](https://developer.salesforce.com/docs/component-library/documentation/en/lwc/lwc.get_started_local_dev_setup) - This is super useful and you don't need DevHub enabled to setup this local server despite what the documentation says. If you want a local server to test your lwc ideas, this really comes in handy.

3) [Salesforce LWC Dev Mobile CLI Plugin](https://github.com/forcedotcom/lwc-dev-mobile) - This cli plugin allows you to demo your lwc's in an iOS emulator or an Android emulator (you need those emulators installed on your machine via XCode and Android Studio). Useful when demoing or testing mobile apps.

4) [Prettier Code Formatter VSCode Plugin](https://developer.salesforce.com/tools/vscode/en/user-guide/prettier) - This allows you to auto-format your code however you'd like it. There is also an apex plugin for prettier which makes this whole setup a bit easier.

5) There are like 10 more I'll list in here eventually.

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