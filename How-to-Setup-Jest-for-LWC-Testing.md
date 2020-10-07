Install/Setup guide for Jest:

1) Download nodejs here: [Node JS Install](https://nodejs.org/en/download/) or use chocolately and nodist if you know what you're doing (this approach is a bit better imo): [NodeJS Nodist Install Instructions](https://github.com/nullivex/nodist)

2) run this command in your project to install jest for lwc: sfdx [force:lightning:lwc:test:setup](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_lightning.htm)

        a) This command also adds the __tests__ folders to the .forceignore file which 
        makes sure its not synced to the server.

3) You may need to change your execution policy since jest doesn't register as a known Windows Package currently. Open powershell as an admin and enter the following command: Set-ExecutionPolicy Unrestricted

        a) When prompted, type the value A and then hit enter

4) Create a folder inside your lightning web component (or Aura Component) folder called \_\_tests\_\_

        a) This can be automatically done by utilizing the sfdx [force:lightning:lwc:test:create](https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_force_lightning.htm) command

        b) If your javascript or the apex it calls does callouts to external systems, also make a folder 
           called __mocks__ to put mock files/classes in

6) Create tests in the \_\_tests\_\_ folder and name them [fileYouAreTesting].test.js

7) Use the cli command npm run test:unit to run tests inside your \_\_tests\_\_ folders

       a) Use the command npm run test:unit:watch to have jest automatically run tests when they get updated. 

[More info on sfdx-lwc-jest here](https://github.com/salesforce/sfdx-lwc-jest)
