Written By: Matt Gerry

This document will outline the standards and best practices I have found to be most useful throughout my time as a SF developer. These are in addition to the typical [Salesforce best practices.](https://developer.salesforce.com/blogs/developer-relations/2015/01/apex-best-practices-15-apex-commandments.html)

I highly suggest you read the following books: 

[Advanced Apex Programming](https://www.amazon.com/Advanced-Apex-Programming-Salesforce-Appleman/dp/1936754126/ref=pd_sbs_14_1/134-8572035-4729812?_encoding=UTF8&pd_rd_i=1936754126&pd_rd_r=e091eb23-daa8-4013-9c17-a9c2678b783c&pd_rd_w=qma8j&pd_rd_wg=r0cF6&pf_rd_p=52b7592c-2dc9-4ac6-84d4-4bda6360045e&pf_rd_r=02MZS6R5D27AGW8EEC0T&psc=1&refRID=02MZS6R5D27AGW8EEC0T)

[Salesforce Lightning Platform Enterprise Architecture - Third Edition](https://www.amazon.com/Salesforce-Lightning-Platform-Enterprise-Architecture/dp/1789956714)



<hr/>
<h1 align="center">
Naming Conventions
</h1>

All conventions outlined below apply to both apex and javascript. Please ensure your javascript follows all these conventions as well.

### _<u>Class file naming</u>_

- Prefix classes with business unit specific logic with appropriate business unit namespaces: BusinessUnit_ClassName. to make it easier to identify code for a particular business unit.

- Prefix classes that are to be utilized as utility classes org wide (without respect to any particular business unit) with the word Util: Util_ClassName. This makes it easier to identify utilities that can be leveraged by everyone working in the org and helps reduce code duplication.

- Use camel case for class names. All words in a class name should be capitalized.

- Always append test classes with _Test, this will make classes and test classes sort next to each other in file lists.

- Class names **MUST BE MEANINGFUL!** Please ensure the name of your class is relevant to the class and what its purpose is.

```
BusinessUnit_MeaningfulClassName
BusinessUnit_MeaningfulClassName_Test
```

### _<u>Method naming conventions</u>_

Methods should utilize camel case conventions. The first word in the method should be lower case, all other uppercase. Method names **MUST BE MEANINGFUL**. They must be named something relevant to the operation they are attempting to execute.

```java
public void methodName(String acctName)
{

}

```

### _<u>Variable naming conventions</u>_

Variables should utilize camel case conventions. The first word in the variable should be lower case, all other uppercase. Variable names **MUST BE MEANINGFUL** they should never be a single character or named something not relevant.

```java
String acctName = 'the name of an account';

```

<hr/>

<h1 align="center">
Code Formatting
</h1>

All of the below applies to both apex and javascript.

### _<u>Brackets<u>_
Always place brackets on their own lines, never place them on the same line. It allows the code to be more readable and for bracket related issues to be easily resolved in any IDE.

Also, **PLEASE WRAP ALL IF STATEMENTS IN BRACKETS!** I know that this is not always necessary but from a readability and debugging stand point it makes things ten times easier. Please always use brackets for if statements.

Bracket Examples:

```java
//Class brackets
public class Brackets
{
  //Code here
}

//Method brackets
public void insertAccounts(List<Account> accounts)
{
  insert accounts;
}

//if statement, case blocks, etc. brackets
if(needsABracket)
{

}
```
### _<u>If Statements or Switch Statements or Ternary Operators?<u>_

Please opt to use if statements over ternary operators. I know ternary operators are simpler to write, but they make code very difficult to read. If statements are very readable even for junior developers where as ternary operators can confuse many developers and take longer to read.

I also prefer if statements over switch statements. I believe if statements are still much more readable.

```java

Boolean shouldBeChecked = null;

//If else example.
//More lines, but very readable
if(checkIt == 'yea')
{
   shouldBeChecked = true;
}
else
{
    shouldBeChecked = false;
}

//Switch statement example
//Readable but less intuitive in my opinion.
switch on checkIt
{
    when 'yea'
    {
        shouldBeChecked = true;
    }
    else
    {
        shouldBeChecked = false;
    }
}

//Ternary operator example.
//One line but very confusing.
shouldBeChecked = checkIt == 'yea' ? true : false;

```

### _<u>Space or Tabs<u>_

All of the below applies to both apex and javascript.

You had better use tabs dawg. If you use spaces you will not be forgiven. If you don't use proper tab indentation you will not be forgiven.

<hr/>

_**Comments**_

- ### _Always Use ApexDocs Comment Formatting_

[ApexDocs](https://github.com/cesarParra/apexdocs) is a wonderful thing. If it's utilized appropriately you will always have exceptional code documentation and it can all be generated automatically. Please make sure all of your code comments follow the ApexDocs format so that you can auto generate markdown files for wiki documentation for our codebase.

- ### _Class Comment block_
At the top of each class create a comment block that notes the developer name (your email), date and a short description of what the class does, why it was made and where it may be referenced elsewhere in the code. Also be sure to include your JIRA ticket number in the description. If it is the controller for an aura component, vf page or LWC you should state what component it is a controller for.
```java
/**
 * @author matt.gerry@tangocentral.com
 * @date 10/23/2019
 * @description Explains coding standards and best practices. JIRA Ticket: #4444
 */
```

- ### _Method comments_
Above every method there should be a description as to what it does and how it is utilized. It should also contain useful comments about the method. Comments should inform the developers as to why something was coded the way it was and the business justifications for it.

```java
/**
 * @description A description of the method.
 * @param exampleVariable Information about the variable we pass to the method.
 * @return What return do we get from this method and why.
 * @example
 * Boolean exampleBoolean = ExampleClass.exampleMethod('exampleString');
 */
public static Boolean exampleMethod(String exampleVariable)
{
    //Logic and code comments to help understand the business reasoning behind the development
    //choices that were made.
}
```

_**CODE COMMENTS ARE EXTREMELY IMPORTANT!! CODE WILL NOT PASS REVIEWS WITHOUT THEM!!**_

<hr/>


<h1 align="center">
HTML Guidelines and Formatting
</h1>

### _<u>Formatting<u>_

HTML formatting should be done in a similar format to how apex indentation is done to improve readability. The code commenting should be the same as apex or javascript.


```html
<!--
     Written By: Matt.Gerry@tacotastic.com
     JIRA Ticket #4444
     Date: 11/4/2019
     Description: Example html tab indentations
-->

<html>
    <head>
        <script></script>
    </head>

    <div>
        <table>
        </table>
    </div>
</html>
```

### _<u>Javascript<u>_

- If the javascript is not contained in an Aura Component or an LWC, Javascript should be housed in its own static resource file and added to the code via a script tag.

- Javascript should be formatted and commented using the exact same standards as outlined above for apex.

### _<u>CSS<u>_

- CSS should always be housed in its own stylesheet file and referenced in the vf page or Aura component or LWC.

- CSS should never be inline or written directly into the page (except for in exceptionally rare circumstances relating to visualforce to pdf rendering).

<hr/>

<h1 align="center">
Test Classes
</h1>

### _<u>Test method best practices</u>_
- Use testMethod modifier on test methods instead of @isTest above the method signature. It looks quite a bit cleaner.
- Put the test setup method as the first method in the test class before all test methods. Also, always utilize @TestSetup methods for setting up test data.
- Create a test method for every class method no matter what, even if one method will call to
  another method and give you code coverage.
- Always ensure every test method uses at least one assertion to make sure we are not only
  getting code coverage but that our apex classes are returning the results we expect them to
  return.
- Make sure to test for both positive and negative scenarios in your test classes (scenarios that fail and scenarios that don't). 
- Make sure to test bulk scenarios. Testing the creation of one contact in a contact trigger is not sufficient. Test how it handles a load of 10,000 contacts too.

```java
//Test Class
@isTest
public class ExampleClass_Test
{
    @TestSetup
    public static void setupData()
    {
        //setup all data that you will need in multiple test methods here
        //The test setup method has its own set of dml limits and will not affect the dml limits
        //of the other methods. Always utilize the object creator for test classes.
List<User> rmdmUser = ObjectCreator.userCreator('MattyRMDM', 1, null, roleId);
    }

    public static testMethod void methodOne_ValidScenario_Test()
    {
        //This test method tests a valid scenario for the method named "Method One" in our
        //"ExampleClass" apex class.
        //All data setup should happen first in this method by utilizing the object creator class
        Test.startTest();
            //The actual callout to the method should always happen inside a Test.startTest() and
            //Test.stopTest() block. This ensures that all system limits are reset and that we
            //have a clearer picture as to what system limits this method is actually reaching.
        Test.stopTest();

        //After we do our test we should always do a System.assertEquals to ensure we aren't just
        //getting code covered but that we are actually getting the results we expect.
        System.assertEquals(value1, value2);
    }
}
```
- Use the SetupData method to create test data, put it before test methods. Separate setup and non-setup object data to avoid mixed dml statement errors.

- Always use a data factory class to create test data, never build that in the class itself.

- Make sure your data factory can create bulk amounts of data for testing, not just a single object at a time.
```
TestDataFactory.createUsers() ...
```

- Use start test and stop test. This will make sure that limits used by the data setup are not counted against the test. This resets and provides a separate set of limits for the test to use.
```java
Test.startTest();
  //Some code goes here
Test.stopTest();
```

- Use assertions to verify the expected outcome has happened
```java
System.assertEquals(expected, actual);
```

<hr/>

<h1 align="center">
Triggers</h1>
<br/>

Triggers should never house any real logic. Their logic should reside in handler classes. This allows us to better handle issues with logic and identify where a problem resides.

I suggest utilizing the [sfdc-trigger-framework](https://github.com/kevinohara80/sfdc-trigger-framework). It's super light weight and more than enough for the vast majority of orgs.

**_THERE SHOULD NEVER BE MORE THAN ONE TRIGGER PER OBJECT!!!!_**

### _<u>Trigger Structure</u>_

Triggers operate in the following way.
1. They run Before operations, then after operations. Before and after operations occur within the same context.
2. They always operate in chunks of 200 records. So if you send in a batch of 1000 contact updates at the same time, the trigger will fire 5 times. It fires once for every 200 records. This all occurs within the same context.
3. Triggers are re-invoked on record update or record insert actions from flows, workflows and process builders. For this reason it is not ideal to have combined execution types. Either use triggers, flows, workflows or process builders. Combining them can really slow things down and is detrimental in larger orgs. If you do combine them, make sure nothing requires trigger recursion and build mechanisms to shut off the triggers when another process updates or inserts a record.

Please reference the [sfdc-trigger-framework](https://github.com/kevinohara80/sfdc-trigger-framework) documentation to see how to appropriately structure your triggers and their handler classes.

### _<u>Trigger Recursion</u>_
_**TRIGGERS SHOULD NEVER REQUIRE RECURSION**_
If your trigger requires recursion, you have designed your implementation wrong, there is never a need for recursion to happen within a trigger and can have detrimental effects on the environment as a whole.

That being said there are lots of things that can cause a trigger to re-fire such as a process builder updating or inserting a record or a workflow rule updating a record.

To prevent workflows and process builders from recursively firing a trigger we should always implement a way to prevent the recursion from taking place. With the [sfdc-trigger-framework](https://github.com/kevinohara80/sfdc-trigger-framework) you can utilize the bypass method to bypass your trigger when appropriate. 

In the event you have a process builder or workflow on an object that is causing trigger recursion use the apex utility classes provided on this github page to bypass the trigger execution.


### _<u>Trigger Switches</u>_

To ensure we have an easy way to turn our triggers on and off in production in the event of a large data import or an emergency we have implemented a custom setting called trigger switches. These trigger switches allow us to switch our triggers off declaratively without having to redeploy them from a lower environment. **_All triggers should have a trigger switch made for them._** You can create a new trigger switch variable by going to Setup -> Custom Settings ->Trigger Switches -> Create new field

Once you have created the trigger switch, make sure to place code at the top of the trigger that effectively allows you to bypass the trigger if the trigger switch is unchecked.

```java
trigger AccountTrigger on Account (before insert, before update, after update, after insert)
{
    //DO NOT PUT ANY CODE ABOVE THIS LINE!!!!!
    //Determining if the trigger has been turned off via the Trigger Switches Custom Setting
    //Triggers should only be deactivated using the custom setting during large volume data
    //loads.
    Trigger_Switches__c isTriggerOn = Trigger_Switches__c.getOrgDefaults();
    if(!isTriggerOn.AccountTrigger_Switch__c)
    {
        return;
    }

    //All other code goes below this statement.
}
```

If we put all the above rules together we can infer that triggers should always be structured as follows:

```java

//The trigger should always be the name of the object with the post-fix _Trigger
//trigger example
trigger ObjectName_Trigger on Object (dml operations)
{
    //DO NOT PUT ANY CODE ABOVE THIS LINE!!!!!
    //Determining if the trigger has been turned off via the Trigger Switches Custom Setting
    //Triggers should only be deactivated using the custom setting during large volume data
    //loads.
    Trigger_Switches__c isTriggerOn = Trigger_Switches__c.getOrgDefaults();
    if(!isTriggerOn.[Object]Trigger_Switch__c)
    {
        return;
    }

    if(trigger.isBefore)
    {
        //Checking to see if we've run the before trigger within this operational context.
        if(!StaticTriggerVariables.stopBefore[Object]Trigger)
        {
            System.debug('::: The before statement in triggerX is firing :::');

            if(trigger.isInsert)
            {
                // put before insert handler class callouts here
            }
            if(trigger.isUpdate)
            {
                //put before update handler class callouts here
            }

            //this declaration will prevent the account triggers before statement from being
            //called again within the same operating context
            StaticTriggerVariables.stopBefore[Object]Trigger = true;
        }
    }

    if(trigger.isAfter)
    {
        //Checking to see if we've run the after trigger within this operational context.
        if(!StaticTriggerVariables.stopAfter[Object]Trigger)
        {
            System.debug('::: The after statement in triggerX is firing :::');

            if(trigger.isInsert)
            {
                // put after insert handler class callouts here
            }
            if(trigger.isUpdate)
            {
                //put after update handler class callouts here
            }

            //this declaration will prevent the account triggers before statement from being
            //called again within the same operating context
            StaticTriggerVariables.stopAfter[Object]Trigger = true;
        }
    }
}

```
<br/>
<hr/>
<br/>

<h1 align="center">
Process Builders
</h1>
<br/>

Process builders are much like triggers in that there should typically only ever be one of them, however on occasion there can be a maximum of two per object. _**DO NOT MAKE MORE THAN ONE PROCESS BUILDER FOR EACH OF THE TWO TYPES LISTED BELOW!**_ Having more than one for either type can cause unexpected consequences. Build supplemental process builder logic into an existing process builder.

### _<u>Naming Conventions</u>_

Process builders should be named as follows:

Insert Process Builders: [ObjectName] - Record Insert
Insert/Update Process Builders: [ObjectName] - Record Update

[ObjectName] should be replaced with the name of the object the process builder is on.

### _<u>Insert Process Builders</u>_
The first of the two types of process builders is an insert process builder. These process builders are used when an object has actions that should be taken on it **ONLY** when an new record is created for it. So if you specify in the process builder "Only when a record is created" That would qualify as an insert process builder.

### _<u>Insert/Update Process Builders</u>_
The second and most common type of process builder is a process builder that operates on insert and on update. If you make a process builder with the "when a record is created or edited" criteria it would qualify as an Insert/Update process builder.

### _<u>Terminating a Process Builder</u>_
In the event you would like entry criteria for a process builder to terminate all actions the process builder may take without taking any action on any records, please utilize the **_Process_Builder_Terminator_** apex class. Use an apex callout to call the Process_Builder_Terminator to end your process builder without doing anything at all.

### _<u>Process Builder Switches</u>_
As we did with our triggers, process builders also have declarative switches made for them. There is a custom setting for them as well. **_Every object with a process builder should have a Process Builder Switch made for it._**. You do not make one switch per process builder, rather one switch per object that has one or more process builders. This allows us to turn off all process builders for an object quickly. To make a process builder switch go to Setup -> Custom Settings -> Process Builder Switches -> Create new field.

Once you have a switch made for your process builder object, make sure to implement a check to ensure the switch is on in the first node of the process builder. If the switch is not on, terminate the process builder using the apex class Process_Builder_Terminator.

![PBDeclarativeSwitch.PNG](/.attachments/PBDeclarativeSwitch-d9ed0d44-e7eb-44f5-b480-c68cdb81bdf0.PNG)

<hr/>

<h1 align="center">
Workflow Rules
</h1>

Aside from time based event firing, there is really no need to utilize these much anymore. Anything they are capable of can typically be achieved within a process builder or a process builder combined with a flow or an apex class. **IF A PROCESS BUILDER CAN DO IT, USE A PROCESS BUILDER PLEASE.**

<br/>

<hr/>

<h1 align="center">
Error Logging
</h1>

### _<u>How to utilize the custom Error Log Table:<u>_

_**ALL CODE MUST UTILIZE THE ERROR LOGGING TABLE!!**_ This custom error logging table allows us greater insight into the errors that occur, when they occurred and who they occurred for. The error logging should be implemented in both the view and controller (view could be the aura component, LWC or VF Page). You should call the Universal_Error_Logger apex class to insert these error logs.

The custom error logging tables developer name is _**Error_Log__c**_. You need to fill out the following fields in the following ways:

- Displayed_Error__c : The error that was actually displayed to the user (this applies if you have custom error messaging that was simplified for the end user).
- Page_Error_Occured__c: This should be the name of the view or controller that the error occurred on.
- SF_Error_Detail__c: This should be the true system generated error that happened.
- User__c: This field should always be filled out with the Id of the operating user which you can get by using the UserInfo.getUserId() method.

_**Apex Example:**_

```java
public String insertAcctRecord(Account acct)
{
    String returnUIMsg = null;  

    try
    {
        database.insert(acct);
        returnUIMsg = 'Account Successfully Inserted';
    }
    catch(Exception ex)
    {
        returnUIMsg = 'There was an error inserting your account';
        Universal_Error_Logger.auraGenerateErrorLog(returnUIMsg, 'insertAcctRecord',
        ex.getMessage());
    }

    return retunUIMsg;
}

```

_**Aura Example**_

There is a component named UniversalErrorLogger that we will add to our component to allow this to be relatively abstract.

_**Component**_
```html
<aura:component description="Example Component" controller="exampleController">

    <!-- Here we are importing the universal error logging component
     so that we can record errors when they happen in our error logging
     object/table and inform admins-->
    <c:UniversalErrorLogger aura:id="errorLogger"/>

    <aura:attribute name="errorList" type="List"/>

</aura:component>
```

```javascript
exampleMethod : function(component, event, helper)
{
        var exampleCallout = component.get("c.controllerMethod");
        exampleCallout.setCallback(this, function(response)
        {
            var state = response.getState();
            if(state === 'SUCCESS')
            {
                var returnVal = response.getReturnValue();
                console.log('Return Value ::: ' + returnVal);
            }
            else if(state == 'ERROR')
            {
                component.set("v.errorList", response.getError());
                helper.sendErrorToAdmins(component, event, helper);
            }
        });
        $A.enqueueAction(addCRMember);
    },

    sendErrorToAdmins : function(component, event, helper)
    {
        //Getting our errors and feeding them into a string (while it's possible multiple errors can be returned
        //the first error is typically the most useful error). If we find we need to return more info we can expand this later.
        var errorsCombined = '';
        var errorList = component.get("v.errorList");
        if (errorList)
        {
            if (errorList[0] && errorList[0].message)
            {
                errorsCombined = errorList[0].message;
                console.log("Error message: " + errorList[0].message);
            }
            else
            {
                errorsCombined = 'Unknown server error';
            }
        }

        //Finding our UniversalErrorLogger component using the aura:id. The reference to this child component is in the CRM_Mapping_Tool component at the top of the page.
        //We use that reference here to grab it
        var errorComponent = component.find("errorLogger");

        //Calling the submitErrorLog method inside the UniversalErrorLogger components component and passing it variables
        errorComponent.submitErrorLog(errorsCombined, 'ERROR', 'ExampleComponent');
    }

```

<hr/>

<h1 align="center">
Security
</h1>

### _<u>Apex With Sharing</u>_

Aside from very specific use cases, please do your best to always utilize the "with sharing keyword in your apex classes to ensure that the internal sharing rules for the user currently running the code are enforced.

```java
//Sharing rules enforced for the use
public with sharing class exampleClass
{

}
```

### _<u>Using the sObject Describe Class for increased security:</u>_

In practice I find this is really only necessary in several situations.

- When doing VF Remoting
- Calling controllers that don't have with sharing enabled from aura or lightning components.
- When most of an apex controller is required to operate in system context but some pieces need enhanced security to proceed.

There are probably more scenarios out there, but these have been the most prevalent for me. If you find yourself in any of those situations, then you need to utilize the sObject describe class to secure your data.

```java
@RemoteAction
webservice static String insertAccount(Account acct)
{
    // checks to see if the running user has permissions to create an account
    if(Schema.sObject.Account.isCreateable())
    {
        database.insert(acct);
    }
}

@RemoteAction
webservice static String updateAccount(Account acct)
{
    // checks to see if the running user has permissions to update an account
    if(Schema.sObject.Account.isUpdateable())
    {
        database.update(acct);
    }
}

@RemoteAction
webservice static String deleteAccount(Account acct)
{
    // checks to see if the running user has permissions to delete an account
    if(Schema.sObject.Account.isDeletable())
    {
        database.delete(acct);
    }
}

@RemoteAction
webservice static String getAccount()
{
    // checks to see if the running user has permissions to read an account
    if(Schema.sObject.Account.isAccessible())
    {
        Account acct = [SELECT Id FROM Account LIMIT 1];
        return acct;
    }
}
```

_**Preventing SOQL Injections**_

_**ALL INPUT FROM AN END USER OR INPUT THAT COULD BE TAMPERED WITH BY AN END USER NEED TO BE SECURED IN THE SERVER SIDE CONTROLLER CODE!!!**_ So let's talk about how to do that shall we?????

The best way to prevent SOQL inject is to utilize the escapeSingleQuotes method on variables that have been passed from the client side to the server side.

```java
@AuraEnabled
public static List<Account> getSomeAccounts(String acctName, String acctState)
{
    //Escaping all quotes to make sure SOQL injection can't happen from user provided input.
    String escapedAcctName = String.escapeSingleQuotes(acctName);
    String escapedAcctState = String.escapeSingleQuotes(acctState);

    List<Account> acctsToReturn = [SELECT Id FROM Account WHERE Name = :escapedAcctName AND BillingState = :escapedAcctState];
}

```

_**More Secure Coding Stuff**_

There are literally tons and tons of things I could write up about this but I'm getting tired. Please ensure you follow all of [Salesforce's secure coding guidelines](https://developer.salesforce.com/docs/atlas.en-us.secure_coding_guide.meta/secure_coding_guide/secure_coding_guidelines.htm) when you are developing. It is extremely important we don't open ourselves up to attacks.

[Salesforce Coding Guidelines](https://developer.salesforce.com/docs/atlas.en-us.secure_coding_guide.meta/secure_coding_guide/secure_coding_guidelines.htm)

<hr/>


<h1 align="center">
General Coding Guidelines/Principles
</h1>

- No SOQL queries inside loops.
- Opt for multiple queries rather than inner queries (in most cases multiple queries are better).
- Utilize Maps instead of nested for loops. Nested for loops drastically decrease operational speeds.
- Don't expose critical information to the client side (aka no critical info passed to a javascript controller). All critical information should be housed in a server side controller.
- Any input from a user should be processed by a controller to ensure no malicious activity can make it through. For example any user input or any value (including url variables) that can be altered by a user that is utilized in a soql query should have the escapeSingleQuotes method utilized on it to ensure SOQL injections can't occur.
- Utilize the "with sharing" keyword on your apex classes to make sure that end users can only access what they are supposed to access.
- Custom metadata should be used to store connection credentials for API integrations.
- Custom Settings should be leveraged to make code extremely dynamic and malleable.
- **Make sure your code is abstract enough for the future**. If your code can't change at the speed of light, you have coded it wrong. If it's not dynamic enough all of our lives will eventually become a nightmare.



