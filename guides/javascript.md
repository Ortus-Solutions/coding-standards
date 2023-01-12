# Ortus JavaScript Style Guide(){

This guide was re-purposed for the Ortus Solutions team from the original author **Airbnb** (https://github.com/airbnb/javascript)

<a name='TOC'></a>

## Table of Contents

  1. [Types](#types)
  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Functions](#functions)
  1. [Properties](#properties)
  1. [Variables](#variables)
  1. [Hoisting](#hoisting)
  1. [Conditional Expressions & Equality](#conditionals)
  1. [Blocks](#blocks)
  1. [Comments](#comments)
  1. [Whitespace](#whitespace)
  1. [Leading Commas](#leading-commas)
  1. [Semicolons](#semicolons)
  1. [Type Casting & Coercion](#type-coercion)
  1. [Naming Conventions](#naming-conventions)
  1. [Accessors](#accessors)
  1. [Constructors](#constructors)
  1. [Events](#events)
  1. [jQuery](#jquery)
  1. [ES5 Compatibility](#es5)
  1. [Performance](#performance)
  1. [Resources](#resources)
  1. [License](#license)

## <a name='types'>Types</a>

  - **Primitives**: When you access a primitive type you work directly on its value

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    var foo = 1,
        bar = foo;

    bar = 9;

    console.log( foo, bar ); // => 1, 9
    ```
  
  - **Complex**: When you access a complex type you work on a reference to its value

    + `object`
    + `array`
    + `function`

    ```javascript
    var foo = [ 1, 2 ],
        bar = foo;

    bar[ 0 ] = 9;

    console.log( foo[ 0 ], bar[ 0 ]); // => 9, 9
    ```

> **Please make note of the spacing and alignments.**

**[[⬆]](#TOC)**

## <a name='objects'>Objects</a>

  - Use the literal syntax for object creation.

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

  - Don't use [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) as keys.


    ```javascript
    // bad
    var superman = {
      class     : 'superhero',
      default   : { clark : 'kent' },
      private   : true
    };

    // good
    var superman = {
      klass     : 'superhero',
      defaults  : { clark : 'kent' },
      hidden    : true
    };
    ```

> **Please make note of the spacing and alignments.**

**[[⬆]](#TOC)**

## <a name='arrays'>Arrays</a>

  - Use the literal syntax for array creation

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [ 1, 2, 3 ];
    ```

  - If you don't know array length use Array#push.

    ```javascript
    var someStack = [];

    // bad
    someStack[ someStack.length ] = 'abracadabra';

    // good
    someStack.push( 'abracadabra' );
    ```

  - When you need to copy an array use Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)


    ```javascript
    var len = items.length,
        itemsCopy = [],
        i;

    // bad
    for( i = 0; i < len; i++ ){
        itemsCopy[ i ] = items[ i ];
    }

    // good
    itemsCopy = items.slice();
    ```

  - To convert an array-like object to an array, use Array#slice.

```javascript
function trigger(){
    var args = Array.prototype.slice.call( arguments );
    ...
}
```

> Please note spacing when declaring arrays.

**[[⬆]](#TOC)**


## <a name='strings'>Strings</a>

  - Strings longer than 80 characters should be written across multiple lines using string concatenation (`+`).
  - **Note**: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40)

    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that \
    was thrown because of Batman. \
    When you stop to think about \
    how Batman had anything to do \
    with this, you would get nowhere \
    fast.';


    // good
    var errorMessage = 'This is a super long error that ' +
      'was thrown because of Batman.' +
      'When you stop to think about ' +
      'how Batman had anything to do ' +
      'with this, you would get nowhere ' +
      'fast.';
    ```

  - When programatically building up a string, use Array#join instead of string concatenation. Mostly for IE: [jsPerf](http://jsperf.com/string-vs-array-concat/2).

    ```javascript
    var items,
        messages,
        length, i;

    messages = [
        {
            state   : 'success',
            message : 'This one worked.'
        },
        {
            state   : 'success',
            message : 'This one worked as well.'
        },
        {
            state   : 'error',
            message : 'This one did not work.'
        }
    ];

    length = messages.length;

    // bad
    function inbox( messages ){
      items = '<ul>';

      for( i = 0; i < length; i++ ){
        items += '<li>' + messages[ i ].message + '</li>';
      }

      return items + '</ul>';
    }

    // good
    function inbox( messages ){
      items = [];

      for( i = 0; i < length; i++ ){
        items[ i ] = messages[ i ].message;
      }

      return '<ul><li>' + items.join( '</li><li>' ) + '</li></ul>';
    }
    ```

> Please note the whitespacing


**[[⬆]](#TOC)**


## <a name='functions'>Functions</a>

  - Function expressions:

```javascript
// anonymous function expression
var anonymous = function(){
	return true;
};

// named function expression
var named = function named(){
	return true;
};

// immediately-invoked function expression (IIFE)
( function(){
	console.log( 'Welcome to the Internet. Please follow me.' );
} )();
```

  - Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.
  - **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement. [Read ECMA-262's note on this issue](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

```javascript
// bad
if( currentUser ){
	function test(){
		console.log( 'Nope.' );
	}
}

// good
if( currentUser ){
	var test = function test(){
		console.log( 'Yup.' );
	};
}
```

  - Never name a parameter `arguments`, this will take precedence over the `arguments` object that is given to every function scope.

```javascript
// bad
function nope( name, options, arguments ){
  // ...stuff...
}

// good
function yup( name, options, args ){
  // ...stuff...
}
```

> **Please make note of the spacing requirements**

- If you have more than 4 arguments, then break them into separate lines for readability, alongside the whitespacing:

```javascript
// bad
function nope( name, options, arguments, collection, index ){
  // ...stuff...
}

// good
function yup( 
    name, 
    options, 
    arguments,
    collection,
    index
){
  // ...stuff...
}
```


- Always use JSDoc (http://en.wikipedia.org/wiki/JSDoc) style commenting on all functions including closures if necessary:

```javascript
/**
* The hint of the function
* @constructor
* @deprecated
* @see Object
* 
* @name The name argument
* @options The options argument
* @test The Test argument
*
* @return String
*/
function nope( name, options, test ){
  // ...stuff...
}

```

**Please note the space left between the method annotations and the argument annotations and the return annotations**


**[[⬆]](#TOC)**



## <a name='properties'>Properties</a>

  - Use dot notation when accessing properties.

```javascript
var luke = {
  jedi  : true,
  age   : 28
};

// bad, unless this is a dynamic variable
var isJedi = luke[ 'jedi' ];

// good, as it is more legible
var isJedi = luke.jedi;
```

  - Use subscript notation `[]` when accessing properties with a variable.

```javascript
var luke = {
	jedi  : true,
	age   : 28
};

function getProp(prop){
  return luke[ prop ];
}

var isJedi = getProp( 'jedi' );
```

**[[⬆]](#TOC)**


## <a name='variables'>Variables</a>

  - Always use `var` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. Captain Planet warned us of that.

```javascript
// bad
superPower = new SuperPower();

// good
var superPower = new SuperPower();
```

  - Use one `var` declaration for multiple variables and declare each variable on a newline. Try also to align assignments for better readability.

```javascript
// bad
var items = getItems();
var goSportsTeam = true;
var dragonball = 'z';

// good
var items        = getItems(),
    goSportsTeam = true,
    dragonball   = 'z';
```

  - Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

```javascript
// bad
var i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
var i, items = getItems(),
    dragonball,
    goSportsTeam = true,
    len;

// good
var items        = getItems(),
    goSportsTeam = true,
    dragonball,
    length,
    i;
```

**[[⬆]](#TOC)**


## <a name='hoisting'>Hoisting</a>

  - Variable declarations get hoisted to the top of their scope, their assignment does not.

```javascript
// we know this wouldn't work (assuming there
// is no notDefined global variable)
function example(){
	console.log( notDefined ); // => throws a ReferenceError
}

// creating a variable declaration after you
// reference the variable will work due to
// variable hoisting. Note: the assignment
// value of `true` is not hoisted.
function example(){
	console.log( declaredButNotAssigned ); // => undefined
	var declaredButNotAssigned = true;
}

// The interpreter is hoisting the variable
// declaration to the top of the scope.
// Which means our example could be rewritten as:
function example(){
	var declaredButNotAssigned;
	console.log( declaredButNotAssigned ); // => undefined
	declaredButNotAssigned = true;
}
```

  - Anonymous function expressions hoist their variable name, but not the function assignment.

```javascript
function example(){
	console.log( anonymous ); // => undefined
	
	anonymous(); // => TypeError anonymous is not a function
	
	var anonymous = function(){
		console.log( 'anonymous function expression' );
	};
}
```

  - Named function expressions hoist the variable name, not the function name or the function body.

```javascript
function example(){
	console.log( named ); // => undefined
	
	named(); // => TypeError named is not a function
	
	superPower(); // => ReferenceError superPower is not defined
	
	var named = function superPower(){
		console.log( 'Flying' );
	};

	
	// the same is true when the function name
	// is the same as the variable name.
	function example(){
		console.log( named ); // => undefined
		
		named(); // => TypeError named is not a function
		
		var named = function named(){
			console.log( 'named' );
		};
	}
}
```

  - Function declarations hoist their name and the function body.

```javascript
function example(){
	superPower(); // => Flying
	
	function superPower(){
		console.log( 'Flying' );
	}
}
```

  - For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/)

**[[⬆]](#TOC)**


## <a name='conditionals'>Conditional Expressions & Equality</a>

  - Use `===` and `!==` over `==` and `!=`.
  - Conditional expressions are evaluated using coercion with the `ToBoolean` method and always follow these simple rules:

    + **Objects** evaluate to **true**
    + **Undefined** evaluates to **false**
    + **Null** evaluates to **false**
    + **Booleans** evaluate to **the value of the boolean**
    + **Numbers** evalute to **false** if **+0, -0, or NaN**, otherwise **true**
    + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if( [ 0 ] ){
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - Use shortcuts.

    ```javascript
    // bad
    if( name !== '' ){
      // ...stuff...
    }

    // good
    if( name ){
      // ...stuff...
    }

    // bad
    if( collection.length > 0 ){
      // ...stuff...
    }

    // good
    if( collection.length ){
      // ...stuff...
    }
    ```

  - For more information see [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll

**[[⬆]](#TOC)**


## <a name='blocks'>Blocks</a>

  - Use braces with all multi-line blocks.

```javascript
// bad
if( test )
  return false;

// good
if( test ) return false;

// better
if( test ){
  return false;
}

// one liner
if( test ){ return false; }

// bad
function(){ return false; }

// good
function(){
	return false;
}
```

**[[⬆]](#TOC)**


## <a name='comments'>Comments</a>

  - Use `/** ... */` for multiline comments. Include a description, specify types and values for all parameters and return values.

```javascript
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param <String> tag
// @return <Element> element
function make(tag){

  // ...stuff...

  return element;
}

// good
/**
* make() returns a new element
* based on the passed in tag name
*
* @param <String> tag
* @return <Element> element
*/
function make(tag){

  // ...stuff...

  return element;
}
```

  - Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an emptyline before the comment.

```javascript
// bad
var active = true;  // is current tab

// good
// is current tab
var active = true;

// bad
function getType(){
  console.log( 'fetching type...' );
  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}

// good
function getType(){
  console.log( 'fetching type...' );

  // set the default type to 'no type'
  var type = this._type || 'no type';

  return type;
}
```

  - Prefixing your comments with `FIXME` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are `FIXME -- need to figure this out` or `TODO -- need to implement`.

  - Use `// FIXME:` to annotate problems

```javascript
function Calculator(){

	// FIXME: shouldn't use a global here
	total = 0;
	
	return this;
}
```

  - Use `// TODO:` to annotate solutions to problems

```javascript
function Calculator(){
	
	// TODO: total should be configurable by an options param
	this.total = 0;
	
	return this;
}
```

**[[⬆]](#TOC)**


## <a name='whitespace'>Whitespace</a>

- Use soft tabs set to 4 spaces please. No spaces or 2 spaces. TABS

```javascript
// bad
function(){
∙∙var name;
}

// bad
function(){
∙var name;
}

// good
function(){
∙∙∙∙var name;
}
```

- Do not put spaces before opening function braces

```javascript
// bad
function test() {
  console.log( 'test' );
}

// good
function test(){
  console.log( 'test' );
}
```
  

- Put spaces on anything that sourrounds `{}` or `[]` or `()` for readibility. If array or collection assignments are long enough, split into multi-line assignments.

```javascript
// bad
function test() {
    console.log('test');
    i[0,3,5]
    test = {a=1,b=2,c=3,d=4}
}

// good
function test() {
    console.log( 'test' );
    i[ 0, 3, 5 ];
    test = { 
        a = 1, 
        b = 2,
        c = 3,
        d = 4
    };
}
```
  


  - Use indentation when making long method chains.

```javascript
// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// good
$( '#items' )
	.find( '.selected' )
	.highlight()
	.end()
	.find( '.open' )
	.updateCount();

// bad
var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
    .attr('width',  (radius + margin) * 2).append('svg:g')
    .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
    .call(tron.led);

// good
var leds = stage.selectAll( '.led' )
	.data( data )
	.enter().append( 'svg:svg' )
	.class( 'led', true )
	.attr( 'width', ( radius + margin ) * 2 )
	.append( 'svg:g' )
	.attr( 'transform', 'translate(' + ( radius + margin ) + ',' + ( radius + margin ) + ')' )
	.call( tron.led );
```

**[[⬆]](#TOC)**

## <a name='leading-commas'>Leading Commas</a>

  - **Nope.**

```javascript
// bad
var once
  , upon
  , aTime;

// good
var once,
    upon,
    aTime;

// bad
var hero = {
    firstName: 'Bob'
  , lastName: 'Parr'
  , heroName: 'Mr. Incredible'
  , superPower: 'strength'
};

// good
var hero = {
  firstName 	: 'Bob',
  lastName 		: 'Parr',
  heroName 		: 'Mr. Incredible',
  superPower 	: 'strength'
};
```

**[[⬆]](#TOC)**


## <a name='semicolons'>Semicolons</a>

  - **Yup.**

```javascript
// bad
(function(){
	var name = 'Skywalker'
	return name
})()

// good
(function(){
	var name = 'Skywalker';
	return name;
})();

// good
(function(){
	var name = 'Skywalker';
	return name;
})();
```

**[[⬆]](#TOC)**


## <a name='type-coercion'>Type Casting & Coercion</a>

  - Perform type coercion at the beginning of the statement.
  - Strings:

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = '' + this.reviewScore;

    // bad
    var totalScore = '' + this.reviewScore + ' total score';

    // good
    var totalScore = this.reviewScore + ' total score';
    ```

  - Use `parseInt` for Numbers and always with a radix for type casting.
  - If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need to use Bitshift for [performance reasons](http://jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you're doing.

    ```javascript
    var inputValue = '4';

    // bad
    var val = new Number(inputValue);

    // bad
    var val = +inputValue;

    // bad
    var val = inputValue >> 0;

    // bad
    var val = parseInt(inputValue);

    // good
    var val = Number( inputValue );

    // good
    var val = parseInt( inputValue, 10 );

    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    var val = inputValue >> 0;
    ```

  - Booleans:

    ```javascript
    var age = 0;

    // bad
    var hasAge = new Boolean(age);

    // good
    var hasAge = Boolean( age );

    // good
    var hasAge = !!age;
    ```

**[[⬆]](#TOC)**


## <a name='naming-conventions'>Naming Conventions</a>

  - Avoid single letter names. Be descriptive with your naming.

    ```javascript
    // bad
    function q(){
      // ...stuff...
    }

    // good
    function query(){
      // ..stuff..
    }
    ```

  - Use camelCase when naming objects, functions, and instances

    ```javascript
    // bad
    var OBJEcttsssss = {};
    var this_is_my_object = {};
    var this-is-my-object = {};
    function c(){};
    var u = new user({
      name: 'Bob Parr'
    });

    // good
    var thisIsMyObject = {};
    function thisIsMyFunction(){};
    var user = new User( {
      name : 'Bob Parr'
    } );
    ```

  - Use PascalCase when naming constructors or classes

    ```javascript
    // bad
    function user(options){
      this.name = options.name;
    }

    var bad = new user({
      name: 'nope'
    });

    // good
    function User( options ){
		this.name = options.name;
    }

    var good = new User( {
		name : 'yup'
    } );
    ```

  - When saving a reference to `this` use `_this`.

```javascript
// bad
	function(){
	var self = this;
	return function(){
		console.log(self);
	};
}

// bad
	function(){
	var that = this;
	return function(){
		console.log(that);
	};
}

// good
function(){
	var _this = this;
	return function(){
		console.log( _this );
	};
}
```

  - Name your functions. This is helpful for stack traces.

```javascript
// bad
var log = function(msg){
  console.log(msg);
};

// good
var log = function log( msg ){
	console.log( msg );
};
```

**[[⬆]](#TOC)**


## <a name='accessors'>Accessors</a>

  - Accessor functions for properties are not required
  - If you do make accessor functions use getVal() and setVal('hello')

```javascript
// bad
dragon.age();

// good
dragon.getAge();

// bad
dragon.age(25);

// good
dragon.setAge( 25 );
```

  - If the property is a boolean, use isVal() or hasVal()

```javascript
// bad
if(!dragon.age()){
  return false;
}

// good
if( !dragon.hasAge() ){
  return false;
}
```

  - It's okay to create get() and set() functions, but be consistent.

```javascript
function Jedi(options){
  options || (options = {});
  var lightsaber = options.lightsaber || 'blue';
  this.set( 'lightsaber', lightsaber );
}

Jedi.prototype.set = function( key, val ){
	this[ key ] = val;
};

Jedi.prototype.get = function( key ){
	return this[ key ];
};
```

**[[⬆]](#TOC)**


## <a name='constructors'>Constructors</a>

  - Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

    ```javascript
    function Jedi(){
      console.log('new jedi');
    }

    // bad
    Jedi.prototype = {
      fight: function fight(){
        console.log('fighting');
      },

      block: function block(){
        console.log('blocking');
      }
    };

    // good
    Jedi.prototype.fight = function fight(){
      console.log( 'fighting' );
    };

    Jedi.prototype.block = function block(){
      console.log( 'blocking' );
    };
    ```

  - Methods can return `this` to help with method chaining.

    ```javascript
    // bad
    Jedi.prototype.jump = function(){
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function(height){
      this.height = height;
    };

    var luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20) // => undefined

    // good
    Jedi.prototype.jump = function(){
      this.jumping = true;
      return this;
    };

    Jedi.prototype.setHeight = function(height){
      this.height = height;
      return this;
    };

    var luke = new Jedi();

    luke.jump()
      .setHeight( 20 );
    ```


  - It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

    ```javascript
    function Jedi(options){
      options || (options = {});
      this.name = options.name || 'no name';
    }

    Jedi.prototype.getName = function getName(){
      return this.name;
    };

    Jedi.prototype.toString = function toString(){
      return 'Jedi - ' + this.getName();
    };
    ```

**[[⬆]](#TOC)**


## <a name='events'>Events</a>

  - When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```js
    // bad
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', function(e, listingId){
      // do something with listingId
    });
    ```

    prefer:

    ```js
    // good
    $( this ).trigger( 'listingUpdated', { listingId : listing.id } );

    ...

    $( this ).on( 'listingUpdated', function( e, data ){
      // do something with data.listingId
    });
    ```

**[[⬆]](#TOC)**

## <a name='jquery'>jQuery</a>

  - Prefix jQuery object variables with a `$`.

```javascript
// bad
var sidebar = $('.sidebar');

// good
var $sidebar = $( '.sidebar' );
```

- Cache jQuery lookups.

```javascript
// bad
function setSidebar(){
	$('.sidebar').hide();
	
	// ...stuff...
	
	$('.sidebar').css({
		'background-color': 'pink'
	});
}

// good
function setSidebar(){
	var $sidebar = $( '.sidebar' );
	$sidebar.hide();
	
	// ...stuff...
	
	$sidebar.css( {
		'background-color': 'pink'
	} );
}
```

- For DOM queries use Cascading `$( '.sidebar ul' )` or parent > child `$( '.sidebar > ul' )`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
- Use `find` with scoped jQuery object queries.

```javascript
// bad
$('.sidebar', 'ul').hide();

// bad
$('.sidebar').find('ul').hide();

// good
$( '.sidebar ul' ).hide();

// good
$ ('.sidebar > ul' ).hide();

// good (slower)
$sidebar.find( 'ul' );

// good (faster)
$( $sidebar[ 0 ] ).find( 'ul' );
```

**[[⬆]](#TOC)**


## <a name='es5'>ECMAScript 6 Compatibility</a>

- Refer to [Kangax](https://twitter.com/kangax/)'s ES5 [compatibility table](http://kangax.github.com/es5-compat-table/)
- Refer to the new 2015 ECMAScript references https://babeljs.io/docs/learn-es2015/
	
**[[⬆]](#TOC)**


## <a name='performance'>Performance</a>

  - [On Layout & Web Performance](http://kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](http://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](http://jsperf.com/try-catch-in-loop-cost)
  - [Bang Function](http://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](http://jsperf.com/jquery-find-vs-context-sel/13)
  - [innerHTML vs textContent for script text](http://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](http://jsperf.com/ya-string-concat)
  - Loading...

**[[⬆]](#TOC)**


## <a name='resources'>Resources</a>


**Read This**

  - [Annotated ECMAScript 5.1](http://es5.github.com/)
  - https://babeljs.io/docs/learn-es2015/

**Other Styleguides**

  - [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
  - [jQuery Core Style Guidelines](http://docs.jquery.com/JQuery_Core_Style_Guidelines)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js/)

**Other Styles**

  - [Naming this in nested functions](https://gist.github.com/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52)

**Further Reading**

  - [Understanding JavaScript Closures](http://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll

**Books**

  - [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](http://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](http://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](http://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](http://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](http://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](http://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch

**Blogs**

  - [DailyJS](http://dailyjs.com/)
  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](http://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](http://weblog.bocoup.com/)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](http://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [Dustin Diaz](http://dustindiaz.com/)
  - [nettuts](http://net.tutsplus.com/?s=javascript)

**[[⬆]](#TOC)**



## <a name='license'>License</a>

(The MIT License)

Copyright (c) 2012 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[[⬆]](#TOC)**

# };

