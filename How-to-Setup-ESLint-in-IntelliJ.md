_### In IntelliJ do the following steps:_

1. Download nodejs here: [Node JS Install](https://nodejs.org/en/download/) or use chocolately and nodist if you know what you're doing (this approach is a bit better imo): [NodeJS Nodist Install Instructions](https://github.com/nullivex/nodist)

1. Open the Terminal Window in IntelliJ

2. Run the command `npm init` 
    * Enter a meaningful name for your package and then press enter
    * Press enter for the version number
    * Enter a meaningful description and then press enter
    * Press enter on entry point
    * Press enter on test command
    * Press enter on git repository
    * Press enter on keywords
    * Enter your name as the Author and then press enter
    * Press enter on License
    * Type yes when asked, "Is this Ok?"
    * You should see a "package.json" file show up in your project directory near the bottom

3. Run the command `npm install eslint --save-dev`

4. Run the command npx eslint --init
    * Select the option, "To check syntax, find problems, and enforce code style", for the question, "How would you like to use ESLint?" and then press 
    enter
    * Select the option, "Javascript modules (import/export)", for the question, "What type of modules does your project use", and then press enter
    * Select the option, "None of these" for the question "Which framework does your project use?", and then press enter
    * Select the option, "No" for the question, "Does your project use TypeScript", and then press enter
    * Select the option, "Browser" for the question, "Where does your code run", and then press enter
    * Select the option, "Answers questions about my style" for the question, "How would you like to define a style for your project?", and then press 
    enter
    * Select the option, "Standard" for the question, "Which style guide do you want to follow", and then press enter.
    * Select the option, "Javascript" for the question, "What format do you want your config file to be in?", and then press enter.
    * Select the option, "Tabs" for the question, "What style of indentation do you use?", and then press enter.
    * Select the option, "Double" for the question, "What quotes do you use for strings?", and then press enter.
    * Select the option, "Unix" for the question, " What line endings do you use?", and then press enter.
    * Select the option, "Yes" for the question, " Do you require semicolons?", and then press enter.
    * A file called, ".eslintrc.js" should show up near the bottom of your project directory
    * Your package.json file should be updated to have the following devDependencies: `"devDependencies": {
    "eslint": "[Current Version Number]"
     }`

5. Run the command `npm install eslint babel-eslint @lwc/eslint-plugin-lwc --save-dev`
    * After running this command your package.json file should update again to include the following lines: `"@lwc/eslint-plugin-lwc": "^0.10.0",
    "babel-eslint": "^10.1.0",`

6. Overwrite your .eslintrc.js file to utilize the one here: [ESLint Config File](https://github.com/Coding-With-The-Force/SalesforceBestPractices/blob/master/.eslintrc.js)

7. In IntelliJ go to File -> Settings -> Languages and Frameworks -> Javascript -> Code Quality Tools -> ESLint
    * Click the, "Manual ESLint configuration" radio button.
    * Node Interpreter should be set to, "Project node(C:\Program Files\nodejs\node.exe)
    * ESLint Package should be set to, "~\IdeaProjects\[ProjectName]\node_modules\eslint"
    * Click the, "Configuration File" radio button and select the configuration that you have within your project [project path\.eslintrc.js]
    * Click the OK button

8. ESLint should now be setup in IntelliJ and auto-detect problems in you JS files.
 
