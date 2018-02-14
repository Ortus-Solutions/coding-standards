# Ortus ColdFusion (CFML) Standards & Best Practices

## <a name='TOC'>Table of Contents</a>

  1. [Introduction](#introduction)
  1. [IDE Tools](#idetools)
  1. [Naming & Conventions](#naming-conventions)
  1. [Abbreviations](#abbreviations)
  1. [Acronyms](#acronyms)
  1. [Package Names](#package-names)
  1. [Class/Component/Interface Names](#object-names)
  1. [Methods](#methods)
  1. [Types](#types)
  1. [Tags](#tags)
  1. [Arguments & Variables](#arguments)
  1. [Constants](#constants)
  1. [Whitespaces](#whitespace)
  1. [Code Blocks](#code-blocks)
  1. [Multi-Argument Declarations](#multi-argument)
  1. [Multi-Argument Function Calls](#multi-function)
  1. [Parenthesis Whitespace](#parenthesis)
  1. [Method Chaining](#method-chaining)
  1. [Object Creation](#object-creation)
  1. [End of Lines](#eof)
  1. [Components](#cfc)
    1. [CFC Documentation](#cfc-documentation)
    1. [CFC Scopes](#cfc-scopes)
    1. [CFC Constructors](#cfc-constructors)
    1. [CFC Var Scoping](#cfc-varscoping)
    1. [CFC Output](#cfc-output)
    1. [CFC Return Types](#cfc-returntypes)
    1. [CFC External Scopes](#cfc-external-scopes)
    1. [CFC Default Arguments](#cfc-default-arguments)
    1. [CFC Inheritance vs Composition](#cfc-inheritance)
  1. [General Best Practices](#general)
  1. [ColdBox Best Practices](#coldbox)


## <a name="introduction">Introduction</a>

This document is intended to be a concise summary of best practices for anyone building CFML applications within the Ortus team. Several external resources used when creating this document. Please note that this is a guideline based on past development experience and industry standards. Please use common sense when applying them and note that this document is ever changing as development trends continue to change.

**[[⬆]](#TOC)**


## <a name="idetools">IDE Tools</a>

We have created several IDE formatter tools and some Sublime packages we use:

* [CFBuilder Formatter](https://drive.google.com/open?id=0B3aRjVTf2SeqNmFBZmZJVjR5TUU)
* [CFBuilder Preferences](https://drive.google.com/open?id=0B3aRjVTf2Seqb2pQMnVIQ0NSLTA)
* [CFBuilder/Eclipse Java Cleanup](https://drive.google.com/open?id=0B3aRjVTf2SeqSUZDbW5UUjVwOU0)
* [CFBuilder/Eclipse Java Formatter](https://drive.google.com/open?id=0B3aRjVTf2SeqSndHZEppUmdQLUU)
* [CFBuilder/Eclipse JavaScript Formatter](https://drive.google.com/open?id=0B3aRjVTf2SeqRlctSDhtZDRoRmM)
* [Sublime Alignment](https://www.granneman.com/webdev/editors/sublime-text/packages/how-to-install-and-use-sublime-alignment/)
* [Sublime Emmet](https://packagecontrol.io/packages/Emmet)
* [Sublime Bracket Highlighter](https://packagecontrol.io/packages/BracketHighlighter)
* [Sublime DockBlockr](https://packagecontrol.io/packages/DocBlockr)
* [Sublime Markdown](https://packagecontrol.io/packages/Markdown%20Preview)
* [Sublime ColdBox Platform](https://packagecontrol.io/packages/ColdBox%20Platform)

**[[⬆]](#TOC)**


## <a name="naming-conventions">Naming & Conventions</a>

Use good names for components, methods, arguments and local variables. This can sometimes be a disaster if developers choose random names or non qualified names for methods, arguments and local variables. Naming is very important and will most of the time document your code. Always remember to use meaningful names and stay away from cryptic abbreviations or naming strategies.


**[[⬆]](#TOC)**


### <a name="abbreviations">Abbreviations</a>

AVOID abbreviations if possible. For example, `calculateSalary()` is a better method name than `calcSalary()`. Although you can use well known abbreviations, please try to avoid them if possible. Here are some *examples* NOT RULES:

-   **acc** for accessibility, as in ButtonAccImpl
-   **auto** for automatic, as in autoLayout
-   **eval** for evaluate, as in EvalBindingResponder
-   **impl** for implementation, as in ButtonAccImpl
-   **info** for information, as in GridRowInfo
-   **num** for number of, as in numChildren
-   **min** for minimum, as in minWidth
-   **max** for maximum, as in maxHeight
-   **nav** for navigation, as in NavBar
-   **regex** for regular expression, as in RegexValidator
-   **util** for utility, as in StringUtil


**[[⬆]](#TOC)**

### <a name="acronyms">Acronyms</a>

Acronyms should be avoided in names, but if they must be used, then treat them with the same Camelcase rules for classes or methods/arguments/variables:

```
-- NOT THIS --
url-scanner.cfc
UrlScanner.cfc
parseHTTPString()
ParseHttpString()

-- DO THIS --
UrlScanner.cfc
parseHttpString()
XmlHttpRequest.cfc
```

* [CFC Tips](http://cfdj.sys-con.com/read/41660.htm)
* [Java Coding Standards](http://www.oracle.com/technetwork/java/javase/documentation/codeconvtoc-136057.html)


**[[⬆]](#TOC)**


  
### <a name="package-names">Package Names</a>

Package names should be unique and in lowercase letters. Underscores may be used or hyphens if necessary. You can package your objects/files using two well known approaches:

1.  By Functionality (Best Practice)
2.  By object types

The best practice is to use packaging by functionality if at all possible. This creates better packaging layout and maintenability. Here is an example from an application's model or business layer folder:

```
- model
  - security
  - remote-api
  - products
  - users
  - conversions
  - util
```


**[[⬆]](#TOC)**


### <a name="object-names">Class/Component/Interface Names</a>

Class/Component/Interface names should be nouns, as they represent most likely things or objects. They should be written in camel case with only the **first** letter capitalized for each word. Use whole words and avoid acronyms and abbreviations if possible. Interfaces should begin with the letter **I**. Base or abstract classes should denote themselves in the name as well as either **BaseClass or AbstractClass**. Examples:

```
-- DO THIS --
URLConverter
RSSReader
Serializable
ISearchEngine
IResults
BaseEntity
AbstractLogger

-- NOT THIS --
urlConverter
rssreader
serializable
iSearchEngine
results
entityToRuleThemAll
ALogger
```


**[[⬆]](#TOC)**



### <a name="methods">Methods</a>

Methods should be verbs, in mixed camel case with the **first** letter lower cased and then each internal first letter of words capitalized. Examples:

```js
-- DO THIS --
run()
doThis()
executeInBackground()
isLocated()

-- NOT THIS --
RUN()
dothis()
executeINBackGround()
ISLocated()
```


**[[⬆]](#TOC)**


### <a name="types">Type Names</a>

All ColdFusion type names in arguments, return types and the like should all be in lower case when they are native ColdFusion types. If they are components they should be the EXACT name of the component. This is extermely important if for some reason the code executes in a case-sensitive system, then the code will not work. ALWAYS have the exact case of components and definitions. If no type is defined, then it is assumed it is uses the **any** type.

``` js
-- DO THIS --
function test( array paths, model.users.User user ){}
boolean function isDone(){}
SecurityService function getSecurityService();

-- NOT THIS --
<CFARGUMENT name="paths" type="ARRAY" >
<cfargument NAME="user" type="model.users.user">
<cffunction name="getSecurityService" returnType="model.security.SECURITYSERVICE">
```


**[[⬆]](#TOC)**


### <a name="tags">CFML Tags, Custom Tags and Attributes</a>

All CFML and custom tags should be writing in lower case form, just like HTML tags. Attributes for CFML tags should follow the same behavior as arguments and variables as seen below. If attributes can all be placed in one line, then do that. However, if they will span and cause breaks, consider breaking the attributes into multiple lines and aligning them to the first attribute. Usually, you can do 2 or 3 in one line, else break. Same goes for method calls.

``` coldfusion
-- DO THIS --
<cfhttp url="...">
<cfabort>
<cfdump var="#session#">
<cfhttp url="#urladdress#" method="GET" resolveurl="Yes" throwOnError="Yes"/>

-- NOT THIS --
<CFHTTP>
<CFABORT>
<CFDump Var="#session#">

-- Unecessary Multi Line --
<cfhttp url="#urladdress#" 
method="GET" 
resolveurl="Yes" 
throwOnError="Yes"/>
```



**[[⬆]](#TOC)**


### <a name="arguments">Arguments and Variables</a>

They should be descriptive lowercase single words, acronyms or abbreviations. If multiple words are necessary they should follow camel case with first letter lowercase. Examples:

``` js
-- DO THIS --
niceLocation = "Miami";
results = "";
avgSalary = "323";

-- NOT THIS --
NICELOCATION = "Miami";
Results = "";
average-salary = "323";
```



**[[⬆]](#TOC)**


### <a name="constants">Constants or Static Variables</a>

They should all be in upper case separated by underscores "\_". Examples:

```js
-- DO THIS --
INTERCEPTOR_POINTS = "";
LINE_SEP = "-";
MAX = "123";

-- NOT THIS --
interceptor-points = "";
line_sep = "d";
max = "123";
```


**[[⬆]](#TOC)**


## <a name="whitespace">Whitespaces</a>

This is more of a convenience for readability and preference, but these are the standards we set forward for consistency.


**[[⬆]](#TOC)**



### <a name="code-blocks">Code Blocks</a>

Code blocks should start in one line and end in another.

```js
// DO THIS
component{
}

try{
}

transaction{

}

thread{

}

for( var x = 1; x lte 10; x++ ){

}

if( false ){
} else if( XX ){
} else {
}

// NOT THIS
component
{
}
try {
}
try
{
}
if( ) {
}
if()
{
}
else{ 
}
```



**[[⬆]](#TOC)**

### <a name="multi-argument">Multi-Argument Declarations</a>

When declaring 4 arguments or more go into multi-line layout

```coldfusion
// DO THIS
function testThis(
	required name,
	required any target,
	boolean isHappy="true",
	any results
	){
  
  ... function here

}

// NOT THIS
function testThis(required name, required any target, boolean isHappy="true", any results){
}
```



**[[⬆]](#TOC)**

### <a name="multi-function">Multi-Argument Function Calls</a>

When calling a function with 4 arguments or more go into multi-line layout:

``` js
// DO THIS
obj.callMethod( 
	target 		= this,
	name 		= "luis",
	results		= true,
	moreData 	= "false" 
); 

// NOT THIS
obj.callMethod( target=this, name="luis", results=true, moreData="false" ); 
```


**[[⬆]](#TOC)**



### <a name="parenthesis">Parenthesis Whitespace</a>

Try to always leave a start and ending whitespace for parenthesis code like in method calls, evaluations, etc.

```js

// DO THIS
obj.callMethod( 
	target 		= this,
	name 		= "luis",
	results		= true,
	moreData 	= "false" 
); 
 
obj.test( this );
obj.setData( 1 * total + 4 );
if( x lt 4 ){
}
for( var x=1; x lte 45; x++ ){
}
return ( structKeyExists( local, "results" ) ? local.results : "null" );

// NOT THIS
obj.callMethod(target=this, name="luis", results=true, moreData="false"); 
obj.test(this);
obj.setData(1*total+4);
if(x lt 4){
}
for(var x=1;x lte 45;x++ ){
}
return(structKeyExists(local,"results")?local.results:"null");
```


**[[⬆]](#TOC)**


### <a name="method-chaining">Method Chaining</a>

When using method chaining and libraries that encourage this, remember that they do it for convenience and also readability. Do not chain for up to 1000 levels, use 2 or 3 and then break.

``` js
// DO THIS
obj.$( "test", this ).$args( 1,2,3,4 ).$results( this )
  .$( "another", method() )
  .$( "another", method());

map( "MyCFC" )
  .toPath( "this.path.Component" )
  .asSingleton();

var c = newCriteria()
  .isEq( "id", arguments.id )
  .createAlias( "orders", "o" )
  .isIn( "o.tags", arguments.tags );

// NOT THIS
obj.$("test", this).$args(1,2,3,4).$results(this).$("another", method() );
map( "MyCFC" ).toPath( "this.path.Component" ).asSingleton();
var c = newCriteria().isEq( "id", arguments.id ).createAlias( "orders", "o" ).isIn( "o.tags", arguments.tags );
```


**[[⬆]](#TOC)**


## <a name="object-creation">Prefer *new* over *CreateObject*</a>

Prefer the `new` declaration over the `createObject` declaration to improve readability:

``` js
// do this
obj = new coldbox.system.testing.TestBox();

// dont this
obj = createObject( "component", "coldbox.system.testing.testBox" ).init();
```


> However, please note that this conventions are only if you are writing libraries. If you are within an ecosystem that provides WireBox Dependency Injection, then **always** prefer WireBox.


**[[⬆]](#TOC)**

## <a name="eof">End of Line on Files</a>

Do not add extra lines to files when ending them:

``` coldfusion
// dont this
component{
.....
}
```


**[[⬆]](#TOC)**



## <a name="cfc">Components</a>

### <a name="cfc-documentation">Documentation</a>

Yes, you will need to document **ALL** of your code, from classes to property definitions to code blocks to arguments. Our preference is to write all logic in script and **not** in tags unless we are targeting a specific CFML Engine.  We leverage [DocBox](https://github.com/Ortus-Solutions/DocBox) for reading, parsing and creating documentation out of all CFCs in an application. Please also refer to the [Custom Anotations](https://github.com/Ortus-Solutions/DocBox/wiki/List-of-Custom-Annotations) that DocBox applies so you can extend the metadata in a CFC. The DockBlockr plugin is magnificent for this.


``` js
/**
* @author Luis Majano
* My component documentation
* goes here in multiple lines if needed
* You can add <a href='http://www.coldbox.org'>links</a> and valid HTML if needed
*/
component accessors="true"{
  
  /**
   * First name of the user
   */
  property name="firstName";
  
  /**
   * Last name of the user
   */
  property name="lastName";

  /**
  * Constructor
  */
  function init(){
    return this;
  }

  /**
  * Submit an order
  * @product The product object
  * @coupon The Coupon code needed
  * @results The results object
  */
  function submitOrder( required product, coupon="", boolean results=true ){
  }
}
```

**[[⬆]](#TOC)**

### <a name="cfc-scopes">Scopes</a>


Components can have instance data that can be placed in two different visibility scopes: **private** and **public**. Private variables are declared in the `variables` scope and public variables in the `this` scope. This means that the variables in the `this` scope will be available for modification from the outside world, while the `variables` scope is not accessible from the outside world directly. 

The only way to manipulate these private variables would be through methods that your object will expose to the outside world. This is called data-hiding or encapsulation. 


#### Use Accessors

Leverage implicit getters and setters in all component declarations instead of creating getters and setters manually, unless you need to add behavior to them:

``` js
component accessors="true"{
  
  property name="firstName";
  property name="lastName";
}
```


Be very careful of when to make internal properties public as you will be violating encapsulation (look at next point). One of the best reasons for making variables public is if they do not change and can act like static constants. If your variable does not meet this criteria, then DO NOT expose it as public.

``` coldfusion
<cfset this.OPTIONS = "add,remove">
<cfset this.NOT_FOUND = '_NOTFOUND_'>
<cfset this.EVENT_CACHEKEY_PREFIX = "cboxevent_event-">
```


> Even though you are treating these variables like final static variables they CAN still be modified as ColdFusion does not support *final or static* variables (Lucee does in 5+). It is more of a convention and agreement to use this approach.

**[[⬆]](#TOC)**

### <a name="cfc-encapsulation">Encapsulation</a>

Encapsulation provides the basis for modularity by hiding information from unwanted outside access and attaching that information to only methods that need access to it. This binds data and operations tightly together and separates them from external access that may corrupt/change them intentionally or unintentionally. Encapsulation is achieved by declaring variables as private in a CFC (`variables` scope). 

This gives access to data to only public/package member functions of the CFC. You can then create their mutators (setters) and accessors (getters) via public methods. Some benefits of encapsulation are:

-   You can keep the exposed API the same while changing how your CFC works internally without breaking any code that uses your CFC
-   Prevents the developer from getting in trouble by violating your internal assumptions about how the instance data works
-   It hides your implementation from the outside world

  
```js
-- THESE ARE GOOD --
stuff = myCFC.getStuff();
myCFC.setStuff( stuff );

-- THESE ARE BAD --
stuff = myCFC.stuff;
myCFC.stuff = stuff;
```

**[[⬆]](#TOC)**

### <a name="cfc-constructors">Constructors</a>

Always have an `init()`` method that acts as your constructor and returns `this` (unless you are building a web services/flash remoting facade). Even if the method has a simple return statement, it is always best practice that every object have a constructor method.

```js
component{
  function init(){
    return this;
  }
}
```

If you are using inheritance then you must call the parent constructor by accessing the `super` scope. 

```js
component extends="BaseConverter"{
  function init(){
    super.init();
    return this;
  }
}
```

**[[⬆]](#TOC)**

### <a name="cfc-varscoping">Var Scoping</a>


Always, always, always use `var` or the `local` scope for local variables inside your methods, including ALL loop counters, temporary variables, queries, etc. This is called **var scoping**. If you do not do this, your component will not be thread-safe. 

This means that if somebody persists (stores) this component in memory, subsequent calls can and will override variables and create all sorts of memory problems. There is an open source project called [http://www.schierberl.com/cfblog/index.cfm/2006/7/20/varScoper-10-release varscoper] that can check all of your components for var scoping issues, even if they are using cfscript. Var scoping applies to methods inside components and also to UDF's/Closures in order to comply with best practices.


```js
-- DO THIS --
<cffunction name="myFunction" access="public" returntype="void" output="false" hint="This methods does nothing">
  <cfset var i = 0>
  <cfset var qGet = "">
  <cfquery name="qGet">
  </cfquery>
  <cfloop from="1" to ="20" index="i">
  </cfloop>
</cffunction>

-- NOT THIS --
<cffunction name="myFunction" access="public" returntype="void" output="false" hint="This methods does nothing">
<cfquery name="qGet">
</cfquery>
<cfloop from="1" to ="20" index="i">
</cfloop>
</cffunction>
```

**[[⬆]](#TOC)**
### <a name="cfc-output">Output From CFCs</a>

Always (*with rare exceptions*) use `output="false"` in your function and components. Do not output directly to the buffer inside a CFC method; instead return a string from the method. The main reason is that you don't want to break encapsulation. By outputting directly to the output stream you assume knowledge of the external environment of the CFC. However, if you return a string then you get the exact same behavior when you do `#myCFC.someHTMLGeneratingMethod()#` but you gain the advantage of not assuming that's how your method will be used. For instance, what if the method that returns the string is used inside of a big `cfscript` block where someone is building a string via concatenation? Everything will break.

```js
<cfcomponent output="false">
<cffunction name="getContent" output="false" access="public" returnType="string">
<cfreturn "This is my content">
</cffunction>
</cfcomponent>
```

**[[⬆]](#TOC)**
### <a name="cfc-returntypes">Return Types & Duck Typing</a>


Use the `returnType` attribute of the functions and the `type` attribute of the argument add documentation and runtime type checking. Also remember that `void` is the return type when your method call does not return anything. 

Duck Typing is when you use the return type or type of `any`. This is a useful technique when dealing with a dynamic language such as ColdFusion. This means that the argument or object returned can be ANYTHING, which then your caller needs to determine what to do with it and what it is based on pre-determined conventions. Usually you will need to document this in a `@return ` annotation within your function call to document the possibilities.

A side effect of not using a strong type is a speed enhancement, since ColdFusion does not check the validity of the types. This side effect should not be used to get more performance, unless absolutely necessary.
This dynamic nature of arguments and return types brings forth great power in a dynamic language, but it also opens holes for runtime exceptions. However, thanks to unit testing, these runtime exceptions should be minimized. So as a followup guideline to duck typing is that you must have unit tests for these components.

**[[⬆]](#TOC)**
### <a name="cfc-external-scopes">Referencing External Scopes</a>

Do not directly reference external scopes, i.e.: session/application/client/server/request variables, inside a CFC. If you reference external scopes you will be breaking the encapsulation and cohesiveness of the component at hand. You have now binded the component to an external scope that must exist in order for this component to work. This also provides difficulties when unit testing.

However, the one exception to referencing external scopes is when building **facades**, especially for web services/flash remoting, in which case ALL references to shared scope variables should be encapsulated within the facade. This means, for instance, passing in the dsn instead of referring to application.dsn when doing database queries. If you do not know what a facade is, then please search for facade pattern to learn more about it. It basically encapsulates a shared scope such as application,session, etc into a CFC.

**[[⬆]](#TOC)**
### <a name="cfc-default-arguments">Default Arguments</a>

In general, non-required arguments of a CFC method should have a default value specified, unless you will be programmatically checking for existence using `structKeyExists(arguments, "key")`, which sometimes is useful.

```js
<cfargument name="isReadOnly" type="boolean" default="false" required="false">
<cfargument name="maxRows" type="numeric" default="10" required="false">
```

**[[⬆]](#TOC)**

### <a name="cfc-inheritance">Inheritance & Composition</a>

Use inheritance only when describing an **is-a** relationship, not for a **has-a** relationship (composition) or for code reuse only. For a nice summary, visit http://cnx.rice.edu/content/m11709/latest/ 

Do not use a component as a huge glorified set of methods and call that code reuse. Components are synonymous to objects, they should have an identity upon themselves. Put in practice your [http://en.wikipedia.org/wiki/Ontology Ontology] skills and define what the CFC will do for you and what is their identity.

Always prefer object composition over inheritance. This is where another component is created or injected as a property of the object at hand. There are several reasons of why to choose composition over inheritance in order to make your designs more flexible and not coupled at compile time, which inheritance does. Composition brings in functionality at runtime as you can switch implementations, etc. Some resources are: 

* http://brighton.ncsa.uiuc.edu/prajlich/T/node14.html
* http://www.artima.com/lejava/articles/designprinciples4.html
* http://guidewiredevelopment.wordpress.com/2008/02/05/favoring-composition-over-inheritance/

**[[⬆]](#TOC)**

## <a name="general">General Best Practices</a>

* Avoid using `Application.cfm` and move to `Application.cfc`. Not only will you get more functionality, but it is a standard. Also, **always** have an `Application.cfc` for your application. If not, CF will search for one and use it's settings and you do not want that.
* Only create Application listener methods that you will use, do not create them as empty functions unecessarily.

**[[⬆]](#TOC)**

### Session Scope Usage
Be very careful when using `session` scoped variables in your applications, especially if used under heavy load or high traffic. Remember that `session` variables are per user and consume memory. If they are misused or you issue `session` variables randomly, your RAM usage will increase exponentially. Consider always having low timeouts for your `session` scopes and always disallowing bots to have `session` variables.  Do not pre-set `session` scoped variables if not necessary. Usually, when somebody logs in, then give memory away.


**[[⬆]](#TOC)**

### Use `cflock` On Shared Resources
Use `cflock` whenever you need to make your code thread safe. This applies to variables in shared scopes such as: `server and application` scope. You sometimes want to even lock `session,request` scope if you are working with framesets, but usually locking `session,request` scope is not necessary anymore. Also remember to use `cflock` whenever you are accessing shared resources, such as file operations, cache operations, etc. 
* Always use a `timeout` and `throwOnTimeout` attributes on the `cflock` tag.
* If you use **exclusive** locks on a resource, make sure that you also provide **readonly** locks when trying to read from such resources.
* Use named locks for locking resources that do not apply to scopes such as `server, application, session, request`. However, please understand that the name of the lock is on a **per server** basis. So make sure the name is unique enough so other applications running on the same server do not collide with it. If they do, you will be providing unecesarry bottlenecks as named locks are global.
* Good locking article: http://www.adobe.com/devnet/server_archive/articles/cf_locking_best_practices.html
* Do not overinflate the code within lock tags. Locking code should only occur on small bits of code and when you are acessing the shared resource. Of course, there are special ocassions to do more than just saving in shared scope, but use it as a rule of thumb.

```coldfusion
-- DO THIS --
<cflock name="FileOperation" timeout="20" throwOnTimeout="true">
<cffile action="write" file="#filePath#" output="#content#">
</cflock>
<!-- application scope is exclusively locked on the cache -->
<cflock type="readonly" scope="application" timeout="10" throwOnTimeout="true">
<cfset myVar = application.cache.getValue("x")>
</cflock>
<cfquery name="variables.qUser" datasource="#request.dsn#">
SELECT FirstName, LastName
FROM Users
WHERE UserID = #request.UserID#
</cfquery>
<cflock scope="application" timeout="2" type="exclusive">
<cfset application.qUser=variables.qUser>
</cflock>
-- NOT THIS --
<cflock name="FileOperation" >
<cffile action="write" file="#filePath#" output="#content#">
</cflock>
<cfset myVar = application.cache.getValue("x")>
<cflock scope="application" timeout="2" type="exclusive">
<cfquery name="application.qUser" datasource="#request.dsn#">
SELECT FirstName, LastName
FROM Users
WHERE UserID = #request.UserID#
</cfquery>
</cflock>
```

**[[⬆]](#TOC)**

### Race Conditions
There will be cases where you need to do a double tests in order to avoid race conditions on shared resources. This strategy can be applied when you need to test, for example, if a resource is created, an object is configured, etc. What this strategy does is provide two if statement criterias that can verify behavior on the resource, squished between a `cflock` tag. This prevents threads that have already entered the locking stage and are waiting execution, to re-execute the locked code.

```coldfusion
-- DO THIS --
<cfif not structKeyExists(application,"controller")>
   <cflock name="mainControllerCreation" timeout="20" throwOnTimeout="true" type="exclusive">
      <cfif not structKeyExists(application,"controller")>
         <cfset application.controller = createObject("component","coldbox.MainController").init()>
      </cfif>
   </cflock>
</cfif>

-- NOT THIS --
<cfif not structKeyExists(application,"controller")>
   <cflock name="mainControllerCreation" timeout="20" throwOnTimeout="true" type="exclusive">
      <cfset application.controller = createObject("component","coldbox.MainController").init()>
   </cflock>
</cfif>
```
As you can see from the previous code snippet, if you do not have the double if statements, then code that is waiting on the lock, will re-execute the creation of the controller object. Therefore, since we can test the resource state, we can provide a multi-thread safety net.

### Do Not Abuse Pound Signs
Pound signs are most often used to output variables to their set values or evaluate them. There are many places where you DO NOT need to place hash signs. This only delays the evaluation and is not best practice. Most likely you will only need to use pound signs when using ''cfoutput'' or when dealing with certain tag attributes that require the evaluation of a variable.

```coldfusion
-- DO THIS --
<cfset name = request.firstname>
<cfif isValid></cfif>
<cfset SomeVar = Var1 + Max(Var2, 10* Var3) + Var4>

-- NOT THIS --
<cfset name = #request.firstname#>
<cfif #isValid#></cfif>
<cfset #SomeVar# = #Var1# + #Max(Var2, 10* Var3)# + #Var4#>
```

**[[⬆]](#TOC)**

### More General Recomendations

* Components are supposed to be objects and have an identity. Always ask yourself what this component's responsibilities are and how will it interact with its surroundings.
* Variables pass in and out of components by **reference** or by value based on the same rules as the rest of CFML. For instance, strings, arrays, numbers, and dates all pass by value, but structures, queries, and all other "complex" objects (including CFC instances) pass by reference.
* Arrays in ColdFusion pass by value in Adobe ColdFusion, so beware of this behavior as it is not the same as in Java or other CFML engines.
* `Duplicate()` and CFWDDX do not work on CFC instances (ColdFusion 7 and below). CFC’s can only be serialized in ColdFusion 8 and with several restrictions. Be careful when serializing objects as the entire object graphs have the potential of being serialized. ColdFusion 9 presents mechanisms to restrict component serializations which helps incredibly.
* When extending a component outside the base component's package, the sub-component does not inherit `package` permissions -- thus, you cannot call `package` methods on other CFCs in the package of the base component from the sub-component.
* You can have a method that has a `returnType` or an argument that has a `type` of a base component and return any component that extends that base component. For example, if `methodA` takes an argument `foo` of type `motorVehicle` and you pass `foo` as an instance of `car`, which extends `motorVehicle` then `methodA` will honor that `car` is a `motorVehicle` when doing type checking on the argument `foo`.
* The previous concept applies to interfaces and inheritance.
* Use interfaces when you want to provide clear API definitions that need to be implemented. They can be good documentation tools and provide compile time checks on your code.
* Use `structKeyExists` instead of `isDefined` when checking for existence.

```js
-- DO THIS --
if( structKeyExists( arguments, "car" ) )
if( arguments.exists( "car" ) )

-- NOT THIS --
if( isDefined("arguments.car") )
```

* Use `cfswitch` instead of `cfif` if you have a specific expression that you can evaluate against and if you will have more than 2 `cfelseif` clauses. Not only does it provide more readability, but your code will make more sense.
* Avoid usage of `iif` if at all possible as it is documented to be slower. However, sometimes it can prove handy.
* Avoid usage of `evaluate()` expressions. They have to be evaluated by the ColdFusion engine and will always run slower. There are times when you will have to use them, especially when doing dynamic concatenations, but try to avoid them at all possible.

```
-- DO THIS --
<cfset value = form[ "field#i#" ]>
-- NOT THIS --
<cfset value = evaluate("form.field#i#")>
```

* Use boolean evaluations

```
-- DO THIS --
<cfif len(firstName)></cfif>
<cfif NOT obj.isEmpty()></cfif>
<cfif query.recordcount></cfif>
<cfif arrayLen(myArray)></cfif>

-- NOT THIS --
<cfif firstName eq ""></cfif>
<cfif obj.isEmpty() eq false></cfif>
<cfif query.recordcount gt 0></cfif>
<cfif arrayLen(myArray) gt 0></cfif>
```

* When you are creating view templates, try to always surround it with `cfoutput` tag, instead of nesting them all over the place.

```
-- DO THIS --
<cfoutput>
<html>
<head>
#head#
</head>
<body>
#leftBar#
#content#
#footer#
</body>
</html>
</cfoutput>

-- NOT THIS --
<html>
<head>
<cfoutput>#head#</cfoutput>
</head>
<body>
<cfoutput>#leftBar#</cfoutput>
<cfoutput>#body#</cfoutput>
<cfoutput>#footer#</cfoutput>
</body>
</html>
```
* Code for portability. Avoid at all costs on hardcoding paths, urls, file locations, etc. If you are using a framework, which you should, they usually provide a way to setup application global variables. If not within a framework context, try to set global variables in a shared scope such as `application` scope once when your application loads and then just grab settings from it. Always believe that your application locations can change. 

**[[⬆]](#TOC)**

## <a name="coldbox">ColdBox Specific Best Practices</a>

* Leverage the `rc and prc` scopes directly instead of referencing the `event` object unless you need default values
* Leverage `var` or `local` scope in the event handlers if those variables will NOT be used in layouts/views
* Leverage the `prc` for data set/read safely within your application. Incoming data through the `rc` is NEVER to be trusted. This should remain as what a client sent into a request.
* Do not mix `local` scope usage and `var` scope declared variables in your handlers. PICK ONE approach.
* Do not create dual performing actions that respond to different HTTP verbs. Like a `list()` action that lists and saves to the database in a post. Create two actions, two concerns.
* Always always always leverage injection via WireBox
* Remember that all event handlers are singletons

**[[⬆]](#TOC)**
