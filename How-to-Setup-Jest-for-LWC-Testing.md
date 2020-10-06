Install/Setup guide for Jest:

1) Download nodejs here: [Node JS Install](https://nodejs.org/en/download/) or use chocolately and nodist if you know what you're doing (this approach is a bit better imo): [NodeJS Nodist Install Instructions](https://github.com/nullivex/nodist)

2) [Install Yarn](https://classic.yarnpkg.com/en/docs/install/#windows-stable)

3) Install sfdx-lwc-jest via the CLI using the command: yarn add -D @salesforce/sfdx-lwc-jest

4) You may need to change your execution policy since jest doesn't register as a known Windows Package currently. Open powershell as an admin and enter the following command: Set-ExecutionPolicy Unrestricted
    a) When prompted, type the value A and then hit enter

5) Create a folder inside your lightning web component (or Aura Component) folder called \_\_tests\_\_
    a) If your javascript or the apex it calls does callouts to external systems, also make a folder called \_\_mocks\_\_ to put mock files/classes in

6) Create tests in the \_\_tests\_\_ folder and name them [fileYouAreTesting].test.js

7) Use the cli command npm run test:unit:watch to have jest automatically run tests when they get updated 

[More info on sfdx-lwc-jest here](https://github.com/salesforce/sfdx-lwc-jest)
