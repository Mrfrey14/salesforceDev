Article in progress...

1) Go to Settings -> Dev Hub and Enable the Dev Hub in your org. Really it's beneficial to just enable every setting in here  

2) Create a new VSCode Salesforce project

3) In your new VSCode project go to the following file: config -> project-scratch-def.json and update it to have the settings and features you need your scratch org to have

4) Run the command palette command: SFDX: Authorize A Dev Hub. This will pop a browser window and let you log in to a Salesforce org.

5) Run the command palette command: SFDX: Create a Default Scratch Org

6) If you want to push your local code and config to the scratch org use the following command: SFDX: Push Source to Default Scratch Org

7) If you want to pull code or config from your scratch org into your local vscode project use the commnand: SFDX: Pull Source from Default Scratch Org

7) If you want to open your scratch org use the command: SFDX: Open Default Org



