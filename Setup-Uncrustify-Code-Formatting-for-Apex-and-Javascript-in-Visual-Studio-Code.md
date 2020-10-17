### How to setup uncrustify for apex and javascript in visual studio code

1) Install [Chocolatey Package Manager](https://www.liquidweb.com/kb/how-to-install-chocolatey-on-windows/) or [NPM](https://nodejs.org/en/download/) 

2) Install [Uncrustify](https://chocolatey.org/packages/uncrustify) by running windows powershell as an admin and entering the following command if using chocolatey package manager : `choco install uncrustify ` or `npm i uncrustify` if using npm

3) Install the [Uncrustify Visual Studio Code plugin](https://marketplace.visualstudio.com/items?itemName=LaurentTreguier.uncrustify)

4) In Visual Studio Code press Ctrl+Shift+P to bring up the command palette and enter the following command: Preferences: Open Settings (JSON). This should open a settings.json file

5) Inside the settings.json file add the following lines: 

    ```java
    "uncrustify.langOverrides": {
        "apex": "JAVA",
        "apex-anon": "JAVA"
    },

    "[apex]": {
        "editor.defaultFormatter": "LaurentTreguier.uncrustify"
     },

    "[javascript]": {
        "editor.defaultFormatter": "LaurentTreguier.uncrustify"
    }
    ```

6) Press Ctrl+S to save the settings file

7) Press Ctrl+Shift+P to bring up the control palette and enter the following command: Uncrustify: Create Default Config. After running that command you should see an uncrustify.cfg file in your project (or you can use the config file I like here: [Matt's Uncrustify Config](https://github.com/Coding-With-The-Force/SalesforceBestPractices/blob/master/uncrustify.cfg))

8) Open the uncrustify.cfg file and update all your settings in it (This is just a nice UI with a ton of different options, so nothing complicated here). Make sure to hit the save button in the top right corner when you are done!

9) Once you finished open a file you would like to have code formatting done to and press Alt+Shift+F

10) Enjoy your auto-formatted code!

 

