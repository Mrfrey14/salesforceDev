Written By: Matt Gerry

This document will outline the standards and best practices I have found to be most useful throughout my time as a SF developer. These are in addition to the typical [Salesforce best practices.](https://developer.salesforce.com/blogs/developer-relations/2015/01/apex-best-practices-15-apex-commandments.html)

I highly suggest you read the following books to build a strong foundation as a developer on the platform: 

[Advanced Apex Programming](https://www.amazon.com/Advanced-Apex-Programming-Salesforce-Appleman/dp/1936754126/ref=pd_sbs_14_1/134-8572035-4729812?_encoding=UTF8&pd_rd_i=1936754126&pd_rd_r=e091eb23-daa8-4013-9c17-a9c2678b783c&pd_rd_w=qma8j&pd_rd_wg=r0cF6&pf_rd_p=52b7592c-2dc9-4ac6-84d4-4bda6360045e&pf_rd_r=02MZS6R5D27AGW8EEC0T&psc=1&refRID=02MZS6R5D27AGW8EEC0T)  
[Salesforce Lightning Platform Enterprise Architecture - Third Edition](https://www.amazon.com/Salesforce-Lightning-Platform-Enterprise-Architecture/dp/1789956714)  
[Clean Code](https://amzn.to/35PuMDU)  
[Clean Architecture](https://amzn.to/35FYo6A)  

DISCLAIMER: These are suggested best practices based on past experiences. You may find better options for your own org. These also may become outdated as technology advanced and while I try to update these as frequently as possible I make no promise they will be up to date. Please only use these as a frame of reference to potentially base your own best practice documentation on, it is still required you do your own research and learning to make sure these best practices fit your orgs needs. 

---

<h1 align="center">
Separation of Concerns
</h1>

This is arguably **THE MOST IMPORTANT THING YOU WILL DO IN YOUR ORG!!! DO NOT IGNORE THE NEED TO IMPLEMENT THIS!!!**. After working in over 20 orgs and making tons of mistakes writing code I can tell you from experience implementing Separation of Concerns (SoC) will absolutely change everything for you. If implemented properly it will massively reduce your codebase, make it considerably easier to make code updates on the fly without being terrified, make your code easier to read, make your code extremely abstract and flexible, unlock the wonders of lightning fast and extremely thorough unit testing among other things. Please please please, do not overlook this in your projects **EVER**!!! If you're like me, you will eventually regret that decision quite a bit and it will ruin a once decent place to be a dev.

I have written an extremely in depth guide that includes video tutorials on how to implement this in Salesforce that [you can check out here](https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki), however I will outline the basics below.

It is my personal opinion that the best and most complete library for implementing Separation of Concerns on the Salesforce Platform is the [Apex Common Library](https://github.com/apex-enterprise-patterns/fflib-apex-common). I have spent countless hours with a variety of libraries and none come close to the completeness of this library and none have comparable community support.

---

### <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/07)-The-Service-Layer" target="_blank">The Service Layer</a>

The Service Layer in your org are a collection of apex classes that house your business logic for different areas of your Salesforce org. All the layers are important, but the service layer is the most critical to implement. Your business logic is something that will constantly change and the need for it to be used in your org will evolve over time. Something that was once only used in a controller will almost certainly eventually be used by something else like a trigger in the future. Therefore Service Layer classes and their methods should absolutely be bulkified unless you have an extremely exceptional circumstance. 

It is critical to implement service classes for the different applications in your org for the following reasons:

1) It will drastically reduce the overall code in your system. If you don't create a bulkified service class to house your business logic, you will almost certainly, at one point or another, have to replicate that business logic somewhere else in your codebase. If you write it as a bulkified service, you won't. 

2) It makes updating ever changing business process super easy. Smoooooooooth like butter. Since everything can connect to it and since there's only one place with that business logic, you don't have to go searching high and low through the code to find all the places you need to update the business logic. This is easily the most beneficial aspect of making a service layer... if you work in enough orgs you'll find that without one, business logic alterations (which are frequent) can kill you.

3) If you structure your service classes for more abstract processes (like email sending) you can make them alter their logic at run time which will also drastically reduce code and force you to segment you service classes into extremely logic chunks (this is a confusing concept we'll cover more later, it's also not necessary to implement so don't get scared away by it).

4) It will come in handy when we get into unit testing and mocking in general in the coming sections. Without these distinct layers, unit testing and mocking becomes impossible (this is a confusing concept we'll cover more later, it's also not necessary to implement so don't get scared away by it).

As you can see, there are massive benefits to the service layer. It is the most critical layer to implement without a doubt, so if your codebase doesn't currently implement a service layer, I would start refactoring code to use a service layer first and worry about the Domain and Selector layers later (but don't forget about them!) 

---


### <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/10)-The-Domain-Layer" target="_blank">The Domain Layer</a>

Ahhh the Domain Layer, this one confuses people, but really it's just a fancy trigger handler (kinda). Domain layer classes should house object specific behavior. So they should absolutely house trigger logic/methods (after insert logic, before update logic, etc), but they should also house methods that aren't specific to trigger operations as well. The example I like to give here is the following: Many objects get tasks created for them in a variety of situations and for each object the way tasks are created is often different. You should put your task creation logic in your domain layer, since it's object specific logic. Then your service classes can call that object specific logic when necessary, your trigger logic can call it or wherever else in your code needs to use it.   

It's important to implement a Domain Layer in your codebase because it allows you to house the behavior of your object in a single place and use it everywhere you need it. This helps in the following ways:

1) Any time you need to access object functionality you only need to access or update a single place in your code. Which makes it easier for devs to know where to write things and where to access special custom built functionality for an object.  

2) It reduces code duplication. Many times I see developers write the exact same (or nearly identical) object specific custom logic in multiple apex controllers or batch classes. If they had just implemented a domain layer they could've accessed that code from all of those places and re-used it in all of those places.

3) Implementing a Domain Layer helps you adhere to Salesforce's suggested best practice of using one and only one technology type (aka only using a trigger or a flow, not both). It encourages developers to put their object specific logic in your domain class and to not stray far away from it.

4) Just like with all the other layers, the Domain class assists with mocking in your test classes. If you're tired of your deploys to production taking 230 minutes, this alone makes using a Domain layer very enticing. 

---

### <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/13)-The-Selector-Layer " target="_blank">The Selector Layer</a> 

The Selector Layer is a simple yet effective layer that not only drastically reduces code in your org, but it also helps to set and enforce security standards for the way data is queried in your codebase as well as set standards for the default fields queried and how the records are ordered. The goal of the selector layer is to have all of your queries for a single object be housed in a corresponding selector class, so for example, all of my queries for the Account object would be in the Account_Selector class. You might still be thinking, "But why should I waste my time on this though" and here are the answers:

1) Many times throughout the lifecycle of an application the default fields that need to be queried for a good portion of your object queried change. If you have dozens (or hundreds) of places in your code where you've written the same inline query, this becomes a nightmare to change. You have to go update that everywhere and it's a pain. On the other hand, if you had just used a selector class you'd only ever update it in one place and you're good to go.

2) Often times you use the exact same query multiple places, what if someday in the future that query isn't selective enough or it needs to select more fields, with a selector you can just update the query in one place and fix it everywhere, without it you have to update each query individually and hope you don't overlook one.

3) Selectors enforce security standards for your codebase. You DO NOT want to be in an all too common situation where the same query in application one enforces FLS and CRUD and yet in another application and identical query doesn't do those things. It leads to confusion, data leaks and much more. Selectors help enforce these standards and force developers to choose when to shut off those security measures instead of just forgetting to use them now and then.

4) Using Selectors gives you the option to mock your selector classes in tests which results in massive speed boosts for your test classes. Tired of it taking 2.5 hours to deploy, mocking is the key to getting some of your life back there.

---

### <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/05)-The-Unit-of-Work-Pattern" target="_blank">The Unit of Work Pattern</a> 

You might be reading this right now and going, "Hey dawg, this isn't a layer, it's a pattern, why's it in here get rid of it you scrub", but just stick with me here. The Unit of Work (UOW) is very important and it should not be overlooked. It's almost its own layer, but not quite. A unit of work wraps all of your DML transactions you are making in your code into one beautiful bundle and executes all the inserts, updates, deletions, etc in one fell swoop. On top of that it sets security standards for your DML executions and it implements standardized save point rollbacks. This layer may be my personal favorite aside from the undeniable star of the show, the Service Layer, so let's find out why it's so incredibly useful:

1) You can easily enforce security standards for your DML operations. If you want to make sure some one has the correct CRUD access on the object or FLS prior to doing a DML operation, by using a unit of work you can easily ensure that happens everywhere. Often times in a code base you can see that this varies from class to class. One class does check for FLS and CRUD, another only checks for CRUD and yet another class does no security checks at all. This is kinda awful and using a unit of work makes this easy to avoid.

2) You can standardize error logging for your DML operations. This is also another area of DML operations that often varies greatly throughout your code. By using a unit of work you can ensure every failure in your DML gets logged in the same way!

3) You can make sure your savepoint rollbacks are consistent and rollback all data in a transaction. Many times when you are inserting and/or updating multiple records across a variety of objects it is in your best interest to rollback your saves if any of those records fail to make their way to the database. This is unfortunately often overlooked, leading to tons of orphaned duplicate records throughout the system. Using a unit of work can completely eliminate this problem by just incorporating rollbacks during the transactions.

4) It also allows you the ability to mock DML transactions in test classes. DML transactions interact with the database and database transactions are easily the longest running transactions in your code. By using a unit of work you can mock these transactions in your test classes which will greatly increase your test class speeds. 

---

<h1 align="center">
Naming Conventions
</h1>

All conventions outlined below apply to both Apex and JavaScript. Please ensure your JavaScript follows all these conventions as well.

### _<u>Class file naming</u>_

- Prefix classes with business unit specific logic with appropriate business unit namespaces: BusinessUnit_ClassName. to make it easier to identify code for a particular business unit.

- Prefix classes that are to be utilized as utility classes org wide (without respect to any particular business unit) with the word Util: Util_ClassName. This makes it easier to identify utilities that can be leveraged by everyone working in the org and helps reduce code duplication. An example of a useful utility class is a class that holds common string values or picklist values in the org (ex: Util_Picklist_Values).

- Prefix class that are abstract that could and should be used by any business unit with the word Org. A good example of an org wide class is a service that is a class that is abstract enough to be used for duplicate management on any object in the org (ex: Org_Duplicate_Management_Service).

- <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/07)-The-Service-Layer" target="_blank">Service Layer</a> classes should be named AreaOfOrg_Service. An example of "AreaOfOrg" is maybe a document generation app you've built for your organization, so the name of the service class would end up being `DocumentGeneration_Service`.  

- <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/10)-The-Domain-Layer" target="_blank">Domain Layer</a>   classes (classes that house your object specific behavior and act as trigger handlers) should just be a plural name of the object it represents. For instance for the Contact object, your Domain class would just be `Contacts`.

- <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/13)-The-Selector-Layer " target="_blank">Selector Layer</a> classes (classes that house your queries in SF) should always be named `ObjectName_Selector`.

- Use camel case for class names. All words in a class name should be capitalized.

- Always append test classes with _Test, this will make classes and test classes sort next to each other in file lists.

- Class names **MUST BE MEANINGFUL!** Please ensure the name of your class is relevant to the class and what its purpose is.

Generic example of a class name with its corresponding test class name:
```
BusinessUnit_MeaningfulClassName
BusinessUnit_MeaningfulClassName_Test
```

---

### _<u>Method naming conventions</u>_

Methods should utilize camel case conventions. The first word in the method should be lower case, all other uppercase. Method names **MUST BE MEANINGFUL**. They must be named something relevant to the operation they are attempting to execute.

```java
public void operationBeingDone(List<String> acctNames)
{

}

```

---

### Method Parameter Types

Aside from controller classes, which should have extremely narrow scope and hardly any code, your method parameters should encourage bulkification. What I mean by this is that your method parameters should be Lists, Sets or Maps. They should be collections and your code in your methods should operate in a bulkified manner. This is important for several reasons, the biggest reason however is that you never know what your code will need to do in the future or where/what it will be called by. Today it's only called by a random lightning component, but maybe tomorrow a trigger needs to use the same code or a batch class. Instead of re-writing the method over and over, just bulkify it once and use it everywhere.  

Acceptable Example Methods:  
```
public static void calculateOpportunityProfits(List<Account> accountsToCalculate)
public static void generateWordDocument(Map<String, SObject> sObjectByName)
```

If your method has more than three parameters being passed to it, you've likely made a mistake somewhere. One of several things has probably happened:

1) Your method is way too big and needs to be broken into smaller methods.
2) You need to create a wrapper object to hold all this data in memory instead of passing a bunch of variables

More often than not #1 is your problem, but sometimes it actually can't be avoided. In these cases I would create a [wrapper class](https://youtu.be/PVZOKm6E82Q) to house my variables so they are easier to pass around.

---

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
While I'm personally a big fan of brackets on their own lines, I think it is more common and easier to read for most developers if brackets are placed inline. I would suggest all brackets being inline instead of on their own new line.

Also, **PLEASE WRAP ALL IF STATEMENTS IN BRACKETS!** I know that this is not always necessary but from a readability and debugging stand point it makes things ten times easier. Please always use brackets for if statements.

Bracket Examples:

```java
//Class brackets
public class Brackets{
  //Code here
}

//Method brackets
public void insertAccounts(List<Account> accounts){
  insert accounts;
}

//if statement, case blocks, etc. brackets
if(needsABracket){

}
```
### _<u>If Statements or Switch Statements or Ternary Operators?<u>_

Please opt to use if statements over ternary operators. I know ternary operators are simpler to write, but they make code very difficult to read. If statements are very readable even for junior developers where as ternary operators can confuse many developers and take longer to read.

I also prefer if statements over switch statements. I believe if statements are still much more readable.

```java

Boolean shouldBeChecked = null;

//If else example.
//More lines, but very readable
if(checkIt == 'yea'){
   shouldBeChecked = true;
}
else{
    shouldBeChecked = false;
}

//Switch statement example
//Readable but less intuitive in my opinion.
switch on checkIt{
    when 'yea'{
        shouldBeChecked = true;
    }
    else{
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

As a general rule you should always comment your code. It's important to document the following things:
1. Why the code was written in the first place. What were the business reasons behind it? What is the class/method actually made to do? Etc.
2. To document complex code and why it has to be complex. Typically code is only complex because of inadequate architecture decisions resulting in loosely coupled data (or something similar to that). It still happens though and when it happens it's important to document that in the code.

- ### _Always Use ApexDocs Comment Formatting_

[ApexDocs](https://github.com/cesarParra/apexdocs) is a wonderful thing. If it's utilized appropriately you will always have exceptional code documentation and it can all be generated automatically. Please make sure all of your code comments follow the ApexDocs format so that you can auto generate markdown files for wiki documentation for our codebase.

For information on how to easily install apexDocs please check out my wiki article here: [How to Install ApexDocs](https://github.com/Coding-With-The-Force/SalesforceBestPractices/wiki/How-to-Install-ApexDocs)

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
Ideally methods should be so small and intuitive that method comments are really not necessary, however, if a method is not small and it is very confusing, there should be a description as to what it does and how it is utilized. It should also contain useful comments about the method. Comments should inform the developers as to why something was coded the way it was and the business justifications for it.

```java
/**
 * @description A description of the method.
 * @param exampleVariable Information about the variable we pass to the method.
 * @return What return do we get from this method and why.
 * @example
 * Boolean exampleBoolean = ExampleClass.exampleMethod('exampleString');
 */
public static Boolean exampleMethod(String exampleVariable){
    //Logic and code comments to help understand the business reasoning behind the development
    //choices that were made.
}
```

_**CODE COMMENTS ARE EXTREMELY IMPORTANT!! YOU WILL FORGET WHAT CODE WAS MADE FOR AND HOW IT WORKS WITHOUT THEM!!**_

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

- If the javascript is not contained in an Aura Component or an LWC (for instance a third party JS library), Javascript should be housed in its own static resource file and added to the code via a script tag or imported appropriately in an LWC or Aura component.

- Javascript should be formatted and commented using the exact same standards as outlined above for apex.

### _<u>CSS<u>_

- CSS should always be housed in its own stylesheet file and referenced in the vf page or Aura component or LWC.

- CSS should never be inline or written directly into the page (except for in exceptionally rare circumstances relating to visualforce to pdf rendering).

<hr/>

<h1 align="center">
Test Classes
</h1>

### _<u>Test method best practices</u>_

TEST CLASSES ARE ARGUABLY THE MOST IMPORTANT THINGS YOU WILL EVER DEVELOP! Yes, they're boring, no they aren't exciting, but they are your saving grace and they are how you ensure your code still works despite the 900 new additions to the code base in the last sprint. Do not skimp on test classes, do not treat them like garbage work you have to do. There will be a day, if you ignore your test classes, that your org will break in horrible ways and could result in absolutely terrible situations. Not only will test classes save you from yourself in the future, but they give you the freedom to refactor your code at will. If you hate your code or just know it could be improved, if you have test classes you trust all you need to do is update the code you want to change, re-run the tests and as long as the tests are still successful you can deploy your refactor without the terror of having broken something critical in your org. Make test classes your best friend plz.

**_Test Class Basics_**
- Use the @isTest decorator above each test method as opposed to the "testmethod" method declaration.
- Put the test setup method as the first method in the test class before all test methods. Also, always utilize @TestSetup methods for setting up test data that will be used in at least 75% of all test methods. It's important to note, any limits you've accumulated in the test setup method will be brought over to your actual test methods. BE VERY WARY OF THAT LIMIT CARRY OVER!
- Create a test method for each path your code could take in each method. This includes failure paths. 
Example:
Class being tested:
```java
public class ClassImTesting{
    public List<Account> getAccounts(Id acctId){
        if(acctId != null){
            return [SELECT Id FROM Account WHERE Id = :acctId];
        }
        else{
             return new List<Account>();
        }
    }
}
```
Class Testing the above class:
```java
@isTest
public class ClassImTestimg_Test{
    @isTest    
    private static void getAccounts_nullAcctId_Test(){
        Test.startTest();
        List<Account> acctsReturned = new ClassImTesting().getAccounts(null);
        Test.stopTest();
        System.assertEquals(0, acctsReturned.size(), 'The code should have returned zero accounts in a null account id scenario');
    }

    @isTest    
    private static void getAccounts_realAcctId_Test(){
        Account acct = new Account(name='KewlAccount');
        insert acct;
        Test.startTest();
        List<Account> acctsReturned = new ClassImTesting().getAccounts(acct.Id);
        Test.stopTest();
        System.assertEquals(1, acctsReturned.size(), 'The code should have returned one accounta in a real account id scenario');
    } 
}
```
- Always ensure every test method uses at least one assertion to make sure we are not only
  getting code coverage but that our apex classes are returning the results we expect them to
  return.
- Make sure to test for both positive and negative scenarios in your test classes (scenarios that fail and scenarios that don't). 
- Make sure to test bulk scenarios. Testing the creation of one contact in a contact trigger is not sufficient. Test how it handles a load of 1000 contacts too (bulk scenarios should be unit tested not integration tested which we'll cover later in this section).

```java
//Test Class
@isTest
public class ExampleClass_Test{
    @TestSetup
    public static void setupData(){
        //setup all data that you will need in multiple test methods here
        //The test setup method has its own set of dml limits and will not affect the dml limits
        //of the other methods. Always utilize the object creator for test classes.
        List<User> rmdmUser = ObjectCreator.userCreator('MattyRMDM', 1, null, roleId);
    }

    public static testMethod void methodOne_ValidScenario_Test(){
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

**_Data Factories_**

- Always use a data factory class to create test data, never build that in the class itself.

- Make sure your data factory can create bulk amounts of data for testing, not just a single object at a time.
```
TestDataFactory.createUsers() ...
```

**_Understanding Test.startTest and Test.stopTest_**  

- Using Test.startTest and Test.stopTest will make sure that limits used by the data setup are not counted against the actual code you are trying to test. This resets and provides a separate set of limits for the test to use and for you to evaluate your test method against. It allows you to see how efficient or inefficient your methods are.

```java
Test.startTest();
  //Some code goes here
Test.stopTest();
```

**_Why use Assertions?_**  

- Use assertions to verify the expected outcome for the scenario your test method is testing actually happened. Without the use of assertions your test classes are effectively worthless. They prove nothing. You should strive to assert the outcome every path your code takes.

```java
System.assertEquals(expected, actual);
```

**_<a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/15)-The-Difference-Between-Unit-Tests-and-Integration-Tests" target="_blank">Unit Tests</a>_**

<hr/>

Unit tests, unit tests, unit tests an overlooked magical unicorn in the world of Salesforce... let me ask you a question? Are often irritated your test classes take forever when you're trying to deploy to production? Does it take 30+ minutes just to deploy? Then let me introduce unit tests! When you're writing tests you often have to make a trade off, would you like your tests to run fast? Or would you like it to cover literally every scenario your code could get into? Unit tests solve this problem because you can have hyper focused tests that test every outcome your methods could theoretically have but still be lightning fast.

I understand some projects run out of time/are short on time and tests are often put on the backburner, but it is my opinion that you should ALWAYS WRITE UNIT TESTS!! Integration tests (the normal tests you're used to writing in SF are integration tests) are great and still necessary to some extent, but unit tests are what you should strive to deliver as a developer, because these tests show you if your methods really work the way you believe they work and they are fast, up to 20x faster, in my personal testing, than an integration test. 

My personal favorite and suggested unit testing/mocking library of choice is Apex Mocks, but there are many others out there that you could leverage.

If you have no idea what unit tests are, no worries fam, I've got you covered. Check out the links below for documentation, examples and much more:

<a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/15)-The-Difference-Between-Unit-Tests-and-Integration-Tests" target="_blank">The Difference Between Unit Tests and Integration Tests</a>
<a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/16)-Unit-Test-Mocks-with-Separation-of-Concerns" target="_blank">Unit Testing and Separation of Concerns</a>  
<a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/17)-Implementing-Mock-Unit-Tests-with-the-Apex-Mocks-Library" target="_blank">Implementing Unit Testing with Apex Mocks</a>


---

**_What Should The Mix of Integration and Unit Tests Be?_**

In my personal opinion they should be about 75/25. Typically 75% of your tests should be unit tests (in an ideal world) and about 25% should be integration tests. The reason for this is, integration tests really only need to test the paths where an integration could take place once. So if class A calls Class B (Class A calling Class B is the integration here, we're not talking about integrating with external systems) when Field C is true then we only need to test that positive scenario in the integration test. Alternatively, the unit tests should test every theoretical path your code can take. It should test what happens when Field C is false, what happens when Field C is null, it should test your error handling, etc, etc, etc. There are easily triple the scenarios to test for unit tests typically.

---

<h1 align="center">
Triggers</h1>
<br/>

Triggers should never house any real logic. Their logic should reside in handler classes. This allows us to better handle issues with logic and identify where a problem resides.

I suggest utilizing the [sfdc-trigger-framework](https://github.com/kevinohara80/sfdc-trigger-framework). It's super light weight and more than enough for the vast majority of orgs. That said, if you have a larger org (more than 500 or so users), your org will likely expand to a larger org or you are working for an ISV (managed package providers), you should use something more robust. My suggestion here is to leverage the Apex Common Library to create Domain Layers for your objects. More info on that here: <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/11)-Implementing-The-Domain-Layer--with-the-Apex-Common-Library" target="_blank">Implementing the Domain Layer with the Apex Common Library</a>   

If you have no idea what a trigger handler class is or what a trigger framework is, check out the video I made covering the topic using the framework mentioned above: [How to Implement a Trigger Framework](https://youtu.be/nmwX0djwG_4)

**_THERE SHOULD NEVER BE MORE THAN ONE TRIGGER PER OBJECT!!!!_**

### _<u>Trigger Structure</u>_

Triggers operate in the following way.
1. They run Before operations, then after operations. Before and after operations occur within the same context.
2. They always operate in chunks of 200 records. So if you send in a batch of 1000 contact updates at the same time, the trigger will fire 5 times. It fires once for every 200 records. This all occurs within the same context.
3. Triggers are re-invoked on record update or record insert actions from flows, workflows and process builders. For this reason it is not ideal to have combined automation types. Either use triggers, flows, workflows or process builders. Combining them can really slow things down and is detrimental in larger orgs. If you do combine them, make sure nothing requires trigger recursion and build mechanisms to shut off the triggers when another process updates or inserts a record.

Please reference the [sfdc-trigger-framework](https://github.com/kevinohara80/sfdc-trigger-framework) documentation to see how to appropriately structure your triggers and their handler classes.

### _<u>Trigger Recursion</u>_
_**TRIGGERS SHOULD NEVER REQUIRE RECURSION**_
If your trigger requires recursion, you have designed your implementation wrong, there is never a need for recursion to happen within a trigger and can have detrimental effects on the environment as a whole.

That being said there are lots of things that can cause a trigger to re-fire such as a process builder updating or inserting a record or a workflow rule updating a record.

To prevent workflows and process builders from recursively firing a trigger we should always implement a way to prevent the recursion from taking place. With the [sfdc-trigger-framework](https://github.com/kevinohara80/sfdc-trigger-framework) you can utilize the bypass method to bypass your trigger when appropriate. 

To prevent flows, workflows and process builders from recursively firing a trigger/domain layer in the Apex Common Library (for larger orgs) check out the documentation on how to do so <a href="https://github.com/Coding-With-The-Force/Salesforce-Separation-Of-Concerns-And-The-Apex-Common-Library/wiki/11)-Implementing-The-Domain-Layer--with-the-Apex-Common-Library" target="_blank">here</a> and use invokable apex to turn them off at the start of your flow and re-enable them at the end of your flow.

---

<h1 align="center">
Automation Processes
</h1>
<br/>

---

<h1 align="center">
Flows
</h1>
<br/>

Flows flows flows, they're powerful, but unbelievable dangerous if not in check, that said you can say the same about code. You've gotta wrangle it in and put lots of rules around it or both code and flows become nightmarish hellscapes. That said, flows have have a couple caveats that code doesn't have (pending you don't supplement your flows with lots of custom code); they don't scale well due to limits, even bulkified flows aren't quite what I'd call bulkified and there are severe limits to UI customization with flows which often come back to crush you. 

So here's the deal, here are my personal rules for flows:

1) If you are a startup/small company with a low budget, you should flow all day and you should thank god they exist (for now) because they reduce budget and time to market substantially. Also a tech savvy startup owner could easily build these themselves and save a lot of money.  

2) If you are an organization that never intends to have more than ~500 users in your org and no objects/tables your flows operates on will likely have more than 10-20k records, you can consider using flows, but be weary if you scale they will likely come back to bite you eventually.  

3) If you are a large org 500+ users, millions or billions of records, you should basically never use flows unless they are heavily augmented with code. Here are the situations I believe flows are useful in for large orgs:   
  * You have a really really simple UI that does not require any really custom css, etc. These happen occasionally and screen flows should be leveraged here when possible. But I'm talkin really simple, like basically no decision points kinda simple.  
  * When you have a massive multi-page LWC. It is beneficial to design your LWC to have flows manage the pagination of the LWC's. It can substantially reduce your overall code and need for future customization.  
  * When you have email automations you need to get done, flows are typically the best way. Apex can do this but auto-launched and record-triggered flows do this fine and I can't complain here. Email = flow all day.  
  * You can consider using record-triggered flows when you have low volume on an object... but I would be hesitant and really think about this. You already have a large object, it could scale and get away from you and changing a flow to a trigger is awful. I've done it many times and it hurts.  
    
Those are my rules personally. Flows are awesome when you're small and potentially a nightmare if used improperly when you're large.

---

<h1 align="center">
Process Builders
</h1>
<br/>

_**DO NOT USE PROCESS BUILDERS! THEY WILL SOON BE DEPRECATED!!!!!**_

However in the event you refuse to take the above advice, the below guidelines should be followed.

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

---

<h1 align="center">
Workflow Rules
</h1>

_**DO NOT USE WORKFLOW RULES! THEY WILL SOON BE DEPRECATED!!!!!**_

Don't use them, thanks, lol.
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



