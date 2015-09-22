# Common Style for JavaScript

> If you have comments on this or **disagree about rules** then
> please reach out to me directly. I want to hear it!

## Table of Contents

**_Basics_**
* [Compliance Levels](#compliance-levels)
* [Ground Rules](#ground-rules)
* [Semicolons](#semicolons)
* [Braces](#braces)

**_Identifiers and Primitives_**
* [Naming Contentions](#naming-conventions)
* [Variable Declarations](#variable-declarations)
* [Objects](#objects)
* [Arrays](#arrays)
* [Strings](#strings)
* [Comments](#code-comments)
* [Constructors](#constructors)

**_Statements and Techniques_**
* [Control-flow](#control-flow)
* [Functions](#function)
* [Conditionals](#conditionals)
* [Type Casting & Coercion](#type-casting--coercion)
* [Ternary Operators](#ternary-operators)
* [Errors](#errors)
* [Exports](#exports)
* [Async](#async-programming)

> [Attribution](#attribution)

## Compliance Levels

### GOOD and BAD
* **always / must**: This is **_mandatory_**. _Seriously_
* **never / must not**: Don't **_ever_** do this. Seriously.

### OK
* **should**: **_Try to_** do this. It is encouraged but not strictly enforced.
* **should not**: **_Try not to_** do this. It is discouraged but not prohibited.

## Ground Rules

- **RULE**: **Always** 2-space soft indents (no tabs)
- **RULE**: **Always** semicolons (with [one exception](#semicolons)).
- **RULE**: **Never use comma first**
- **RULE**: **Never use** `()` around statements like `typeof` or `delete`.

## Semicolons

- **RULE**: Semicolons `;` **must** be added at the end of every statement, **except** when the next character is a closing bracket `}`. In that case, they may be omitted.

``` js
//
// GOOD
//
var f = function add(a, b) {
  if (a == b) { return a * 2 }   // No `;` here.
  return a + b;
};
```

``` js
//
// BAD
//
var f = function add (a, b) {
  return a + b
}
```

**[[â¬†]](#table-of-contents)**

## Braces

- **RULE**: Braces **must** be used in all circumstances. They **may** be used on a single line around simple statements.

``` js
//
// GOOD
//
if (x) { return true }
```

``` js
//
// BAD
//
if (x)
  while (1)
    i ++;
else
  //...
```

``` js
//
// BAD
//
if (x) return true;
```

``` js
//
// BAD
//
if (x)
  return true;
```

<hr>

- **RULE**: Opening Braces **must never** be on a line of their own.
- **Rule**: Closing braces **must never** be followed by a conditional statement

> Vertical screen space is precious, and ease of scanning code
> is more previous.

``` js
//
// GOOD
//
if (x) {
  return true;
}
else {
  return false;
}
```

``` js
//
// BAD
//
if (x)
{
  return true;
}
```

``` js
//
// BAD
//
if (x) {
  return true; }
```

``` js
//
// BAD
//
if (x) {
  return true;
} else {
  return false
}
```

<hr>

- **RULE**: Closing Braces **must always** be on a line of their own unless they also start on that line.

> This makes it easy to see the end of a function or statement

``` js
//
// GOOD
//
return callback && callback({ foo: bar });
```

``` js
//
// GOOD
//
return callback && callback({
  foo: bar
});
```

``` js
//
// BAD
//
return callback && callback({
  foo: bar });
```

``` js
//
// BAD
//
return callback && callback({ foo: bar
  });
```

**[[â¬†]](#table-of-contents)**

## Naming Conventions

- **RULE**: Avoid single letter names. Be descriptive with your naming.

``` js
//
// BAD
//
function q() {
  // ...stuff...
}

//
// GOOD
//
function query() {
  // ..stuff..
}
```

<hr>

- **RULE**: Use camelCase when naming objects, functions, and instances

``` js
//
// BAD
//
var OBJEcttsssss = {};
var this_is_my_object = {};
var this-is-my-object = {};
function c() {};
var u = new user({
  name: 'Bob Parr'
});

//
// GOOD
//
var thisIsMyObject = {};

function thisIsMyFunction() {};

var user = new User({
  name: 'Bob Parr'
});
```

<hr>

- **RULE**: Use PascalCase when naming constructors or classes

``` js
// BAD
function user(options) {
  this.name = options.name;
}

var bad = new user({
  name: 'nope'
});

// GOOD
function User(options) {
  this.name = options.name;
}

var good = new User({
  name: 'yup'
});
```

<hr>

- **RULE**: Use a leading underscore `_` when naming private properties

``` js
// BAD
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';

// GOOD
this._firstName = 'Panda';
```

<hr>

- **RULE**: Saved references to `this` (which is a prototypal object) **must** use `self`.

``` js
function User (options) {
  this.setup();
}

//
// GOOD
//
User.prototype.setup = function () {
  var self = this;

  setTimeout(function () {
    self.ready = true
  }, 1000);
};

//
// BAD
//
User.prototype.setup = function () {
  var that = this;

  setTimeout(function () {
    that.ready = true
  }, 1000);
};
```

<hr>

- **RULE**: Saved references to `this` (which is an arbitrary scope) **should** use `that`.

``` js
//
// BAD
//
function () {
  var self = this;
  return function() {
    console.log(self);
  };
}

//
// BAD
//
function () {
  var _this = this;
  return function() {
    console.log(_this);
  };
}

//
// GOOD
//
function () {
  var that = this;
  return function() {
    console.log(that);
  };
}
```

<hr>

- **RULE**: Functions **should** be named. This is helpful for stack traces.

``` js
//
// OK
//
var log = function(msg) {
  console.log(msg);
};

//
// GOOD
//
var log = function log(msg) {
  console.log(msg);
};
```

**[[â¬†]](#table-of-contents)**

## Variable declarations

- **RULE**: Variables **must** always be declared, prior to use.
- **RULE**: Variable declarations **must** appear at the top of functions, and not inside other blocks. The exception is *for* loops.

> Variable declarations are moved up to the top of the function
> scope anyway, so that's where they belong.

``` js
//
// GOOD
//
function (a, b) {
  var k;

  if (a == b) {
    k = true;
  }
  //...
}

for (var i = 0; i < l; i ++) {
  //...
}
```

``` js
//
// BAD
//
function (a, b) {
  if (a == b) {
    var k = true;
  }
  //...
}
```

<hr>

- **RULE**: Variables **must** always align when they are declared

> This makes it easy to scan what is declared in a single block.

``` js
//
// GOOD
//
var bazz,
    foo,
    bar;
```

``` js
//
// BAD
//
var bazz,
  foo,
  bar;
```

<hr>

- **RULE**: Declare unassigned variables last.

> This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

``` js
//
// BAD
//
var i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

//
// BAD
//
var i, items = getItems(),
    dragonball,
    goSportsTeam = true,
    len;

//
// GOOD
//
var items = getItems(),
    goSportsTeam = true,
    dragonball,
    length,
    i;
```

<hr>

- **RULE**: Variables **should** always be declared in decreasing length.

> This also makes it easier to scan what is declared in a single block (trust me).

``` js
//
// GOOD
//
var reallyLongVar,
    shorterVar,
    fooBar,
    foo;
```

``` js
//
// BAD
//
var fooBar,
    shorterVar,
    foo,
    reallyLongVar;
```

<hr>

- **RULE**: Variable assignments **must** come before declarations.
- **RULE**: Variable assignments **should** align **when convenient** depending on additional length.

> This also makes it easier to scan what is declared in a single block (trust me).

``` js
//
// GOOD
//
var reallyLongVar = 10e3,
    shorterVar    = 5e2,
    fooBar        = 'foobar',
    foo;
```

``` js
//
// OK
//
var reallyLongVar = 10e3,
    shorterVar = 5e2,
    fooBar = 'foobar',
    foo;
```

``` js
//
// BAD
//
var foo,
    reallyLongVar = 10e3,
    shorterVar = 5e2,
    fooBar = 'foobar';
```

<hr>

- **RULE**: Multi-line object literals **must be** assigned outside of multi-line variable declaration blocks.

> It's what god would have wanted.

``` js
//
// GOOD
//
var obj  = { list: [], expired: false },
    bazz = 100,
    foo,
    bar;
```

``` js
//
// GOOD
//
var bazz = 100,
    foo,
    bar,
    obj;

obj  = {
  list: [],
  expired: false
};
```

``` js
//
// BAD
//
var obj  = {
  list: [],
  expired: false
},
    bazz = 100,
    foo,
    bar;
```

``` js
//
// BAD
//
var bazz = 100,
    foo,
    bar,
    obj = {
      list: [],
      expired: false
    };
```

<hr>

- **RULE**: Assignment depending on multi-line functions or multiple functions **must be** assigned outside of multi-line variable declaration blocks.

``` js
//
// GOOD
//
var memo = list.filter(function (i) { return i < 10 }),
    bazz = 100,
    foo,
    bar;
```

``` js
//
// GOOD
//
var bazz = 100,
    memo,
    foo,
    bar;

memo = list.filter(function (i) {
  return i < 10;
}).filter(Boolean);
```

``` js
//
// BAD
//
var memo = list.filter(function (i) {
  return i < 10
}),
    bazz = 100,
    foo,
    bar;
```

``` js
//
// BAD
//
var bazz = 100,
    foo,
    bar,
    memo = list.filter(function (i) {
      return i < 10;
    }).filter(Boolean);
```

``` js
//
// BAD
//
var bazz = 100,
    foo,
    bar,
    memo = list.filter(function (i) { return i < 10 })
      .filter(Boolean);
```

**[[â¬†]](#table-of-contents)**

## Objects

- **RULE**: Single line object **must** have a trailing space after `{` and a leading space before `}`.

``` js
//
// BAD
//
var foo = {bar: 1};
```

``` js
//
// BAD
//
return {bar: 1};
```

``` js
//
// GOOD
//
var foo = { bar: 1 };
```

``` js
//
// GOOD
//
return { bar: 1 };
```

<hr>

- **RULE**: Properties in objects **must** be followed by a `:`

``` js
//
// BAD
//
var foo = { bar:1 };
```

``` js
//
// BAD
//
var foo = {
  bar  : 1,
  bazz : 1
};
```

``` js
//
// GOOD
//
var foo = { bar: 1 };
```

``` js
//
// GOOD
//
var foo = {
  bar: 1,
  bazz: 1
};
```

``` js
//
// GOOD
//
var foo = {
  bar:  1,
  bazz: 1
};
```

<hr>

- **RULE**: Multi-line assignment statements **inside an object literal** are **encouraged.**

> Reduces the number of variables managed and object creation is cheap.

``` js
//
// GOOD
//
return {
  foos: list.filter(function (i) {
    return i.type === 'foo';
  }),
  bars: list.filter(function (i) {
    return i.type === 'bar';
  })
}
```

<hr>

- **RULE**: Use the literal syntax for object creation.

``` js
//
// BAD
//
var item = new Object();

//
// GOOD
//
var item = {};
```

- Using [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) is fine as _it is valid Javascript._

``` js
//
// OK
//
var superman = {
 class: 'superhero',
 default: { clark: 'kent' },
 private: true
};
```

**[[â¬†]](#table-of-contents)**

## Arrays

- **RULE**: Use the literal syntax for array creation

``` js
//
// BAD
//
var items = new Array();

// GOOD
var items = [];
```

<hr>

- **RULE**: If you don't know array length use Array#push.

``` js
var someStack = [];

//
// BAD
//
someStack[someStack.length] = 'abracadabra';

//
// GOOD
//
someStack.push('abracadabra');
```

<hr>

- **RULE**: When you need to copy an array use Array#slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

``` js
var len = items.length,
    itemsCopy = [],
    i;

//
// BAD
//
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}

//
// GOOD
//
itemsCopy = items.slice();
```

**[[â¬†]](#table-of-contents)**

## Strings

- **RULE**: Use single quotes `''` for strings

``` js
//
// BAD
//
var name = "Bob Parr";

//
// GOOD
//
var name = 'Bob Parr';

//
// BAD
//
var fullName = "Bob " + this.lastName;

//
// GOOD
//
var fullName = 'Bob ' + this.lastName;
```

<hr>

- **RULE**: Strings longer than 80 characters should be written across multiple lines using string concatenation.

> If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40)

``` js
//
// BAD
//
var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

//
// BAD
//
var errorMessage = 'This is a super long error that \
was thrown because of Batman. \
When you stop to think about \
how Batman had anything to do \
with this, you would get nowhere \
fast.';

//
// GOOD
//
var errorMessage = 'This is a super long error that ' +
  'was thrown because of Batman.' +
  'When you stop to think about ' +
  'how Batman had anything to do ' +
  'with this, you would get nowhere ' +
  'fast.';

//
// GOOD
//
var errorMessage = [
  'This is a super long error that ',
  'was thrown because of Batman.',
  'When you stop to think about',
  'how Batman had anything to do',
  'with this, you would get nowhere'
  'fast.'
].join(' ');
```

<hr>

- **RULE**: When programatically building up a string, use Array#join instead of string concatenation. Mostly for IE: [jsPerf](http://jsperf.com/string-vs-array-concat/2).

``` js
var items,
    messages,
    length,
    i;

messages = [{
  state: 'success',
  message: 'This one worked.'
}, {
  state: 'success',
  message: 'This one worked as well.'
}, {
  state: 'error',
  message: 'This one did not work.'
}];

length = messages.length;

//
// BAD
//
function inbox(messages) {
  items = '<ul>';

  for (i = 0; i < length; i++) {
    items += '<li>' + messages[i].message + '</li>';
  }

  return items + '</ul>';
}

//
// GOOD
//
function inbox(messages) {
  items = [];

  for (i = 0; i < length; i++) {
    items[i] = messages[i].message;
  }

  return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
}
```

**[[â¬†]](#table-of-contents)**

## Code Comments

- **RULE**: You **should not** use JSDoc.
- **RULE**: Block comments **should only** be used in file headers.
- **RULE**: You **should not** use single-line block comments
- **RULE**: Put an emptyline before a comment.

> Having appropriate space in your code comments makes writing
> complex code easier to read. It's the "almost literate coding"
> approach.

- **REMARK**: JSDoc should be considered **deprecated.** When time is available to improve the `docco`-style comments we have historically used we will replace it all together.

### GOOD
``` js
/*
 * a-js-file.js: This is some file
 *
 * (C) 2013 Whomever
 * MIT LICENSE
 *
 */
```

``` js
//
// ### function myFunction (a, b, c)
// #### @a {string} A variable
// #### @b {boolean} Another variable
// #### @c {object|Array} An object or an array
//
// This is the description to my function.
//
```

``` js
//
// Adding additional padding in your code comments
//
var a = 0;

//
// Along with additional whitespace
//
if (!a) {
  console.log('Makes your code easier to read.');
  console.log('What are you running out of bytes?');
}
```

### OK

``` js
// One line comments
var a = 0;
// and no whitespace
if (!a) {
  console.log('make your code harder to read');
  console.log('seriously.');
}
```

``` js
/*
 * I'm using block comments anywhere but the file header.
 */
```

<hr>

- **RULE**: Use `// FIXME:` to annotate problems.
- **RULE**: Use `// TODO:` to annotate solutions to problems.
- **RULE**: Use `// REMARK:` to annotate possible annotations or open implementation questions (which are not obvious problems).
- **RULE**: Sign these comments with your Github username.

### GOOD

``` js
function Calculator() {

  // FIXME (index zero): shouldn't use a global here
  total = 0;

  return this;
}
```

``` js
function Calculator() {

  // TODO (indexzero): total should be configurable by an options param
  this.total = 0;

  return this;
}
```

### BAD

``` js
function Calculator() {

  // shouldn't use a global here
  total = 0;

  return this;
}
```

``` js
function Calculator() {

  // TODO: total should be configurable by an options param
  this.total = 0;

  return this;
}
```

**[[â¬†]](#table-of-contents)**

## Constructors

- **RULE**: Assign methods to the prototype object. You **must never** overwrite the prototype with a new object completely.

> Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

``` js
function Jedi() {
  console.log('new jedi');
}

//
// BAD
//
Jedi.prototype = {
  fight: function fight() {
    console.log('fighting');
  },

  block: function block() {
    console.log('blocking');
  }
};

//
// GOOD
//
Jedi.prototype.fight = function fight() {
  console.log('fighting');
};

Jedi.prototype.block = function block() {
  console.log('blocking');
};
```

<hr>

- **RULE**: Methods can return `this` to help with method chaining.

``` js
//
// OK
//
Jedi.prototype.jump = function() {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function(height) {
  this.height = height;
};

var luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20) // => undefined

//
// GOOD
//
Jedi.prototype.jump = function() {
  this.jumping = true;
  return this;
};

Jedi.prototype.setHeight = function(height) {
  this.height = height;
  return this;
};

var luke = new Jedi();

luke.jump()
  .setHeight(20);
```

<hr>

- **RULE**: It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

``` js
function Jedi(options) {
  options || (options = {});
  this.name = options.name || 'no name';
}

Jedi.prototype.getName = function getName() {
  return this.name;
};

Jedi.prototype.toString = function toString() {
  return 'Jedi - ' + this.getName();
};
```

**[[â¬†]](#table-of-contents)**

## Control-flow

- **RULE**: Control-flow statements, such as `if`, `while` and `for` **must** have a space between the keyword and the left parenthesis.

> They aren't functions, and thus better distinguished like this.

``` js
//
// GOOD
//
if (a) {
  return true;
}
```

``` js
//
// BAD
//
if(a) {
  return true;
}
```

<hr>

- **RULE**: Eager returns **must be** preferred over `if else` blocks.

> Eager returns simplifies most control-flow, especially more complex and high-level control-flow.

``` js
//
// BAD
//
if (foo) {
  callback(null, 'foo');
}
else {
  callback(null, 'bar');
}
```

``` js
//
// GOOD
//
if (foo) {
  return callback(null, 'foo');
}

callback(null, 'bar');
```

**[[â¬†]](#table-of-contents)**

## Functions

- **RULE**: Anonymous functions **must** have a space between the `function` keyword and the left parenthesis.

> To emphasise the lack of identifier and differentiate them with named functions.

``` js
//
// GOOD
//
function (a, b) {}
```

``` js
//
// BAD
//
function(a, b) {}
```

<hr>

- **RULE**: Named functions **must not** have a space between the function name and the left parenthesis.
- **RULE**: Function calls **must not** have a space between the function name and the left parenthesis.

``` js
//
// GOOD
//
function add(a, b) {}
```

``` js
//
// BAD
//
function add (a, b) {}
```

**[[â¬†]](#table-of-contents)**

## Conditionals

- **RULE**: Multi-line conditional statements **must** be properly indented.
- **RULE**: Newlines in multi-line conditional statements **must** be be followed by a boolean operator or `(`.
- **RULE**: Conditional **should not** contain complex logic.

``` js
//
// GOOD
//
if (something === 'foo' && (somethingElse === 'bar'
    && ohYeahThisToo === 'bazz')) {
  return false;
}
```

``` js
//
// BAD
//
if (something === 'foo' && (somethingElse === 'bar' &&
ohYeahThisToo === 'bazz')) {
  return false;
}
```

``` js
//
// BAD
//
if (something === 'foo' && (somethingElse === 'bar' &&
    ohYeahThisToo === 'bazz') {
  return false;
}
```

``` js
//
// OK
//
if (list.filter(function (i) { return i.ok }).length > 5) {
  return false;
}
```

**[[â¬†]](#table-of-contents)**

## Type Casting & Coercion

- **RULE**: Perform type coercion at the beginning of the statement.

``` js
//  => this.reviewScore = 9;

//
// BAD
//
var totalScore = this.reviewScore + '';

//
// GOOD
//
var totalScore = '' + this.reviewScore;

//
// BAD
//
var totalScore = '' + this.reviewScore + ' total score';

//
// GOOD
//
var totalScore = this.reviewScore + ' total score';
```

<hr>

- **RULE**: Use `parseInt` for Numbers and always with a radix for type casting.

> If for whatever reason you are doing something wild and `parseInt` is your bottleneck and need
> to use Bitshift for [performance reasons](http://jsperf.com/coercion-vs-casting/3), leave a comment explaining why and what you're doing.

**Numbers**

``` js
var inputValue = '4';

//
// OK
//
var val = +inputValue;

//
// BAD
//
var val = new Number(inputValue);

//
// BAD
//
var val = inputValue >> 0;

//
// BAD
//
var val = parseInt(inputValue);

//
// GOOD
//
var val = Number(inputValue);

//
// GOOD
//
var val = parseInt(inputValue, 10);

//
// GOOD
//

//
// parseInt was the reason my code was slow.
// Bitshifting the String to coerce it to a
// Number made it a lot faster.
//
var val = inputValue >> 0;
```

**Booleans**

``` js
var age = 0;

//
// BAD
//
var hasAge = new Boolean(age);

//
// GOOD
//
var hasAge = Boolean(age);

//
// GOOD
//
var hasAge = !!age;
```

**[[â¬†]](#table-of-contents)**

## Ternary operators

- **RULE**: Ternary operators are OK, but **must never be combined**.

> More than one and it's spaghetti.

``` js
//
// GOOD
//
var i = 2,
    x = i > 5 ? i : 0;
```

``` js
//
// BAD
//
var i = 2,
    j = 3,
    x = i > 5 ? j > 4 ? j : i : 0;
```

<hr>

- **RULE**: Multi-line Ternary operators are OK, but **must be single line statements.**.

``` js
  //
  // GOOD
  //
  return foo
    ? foo + 1
    : bar;
```

``` js
  //
  // GOOD
  //
  return foo ? foo + 1 : bar;
```

``` js
  //
  // GOOD
  //
  return foo
    ? function () { return foo + 1 }
    : bar;
```

``` js
  //
  // GOOD
  //
  return err
    ? callback(err)
    : callback();
```

``` js
  //
  // BAD
  //
  return foo ?
    foo + 1 :
    bar;
```

``` js
  //
  // BAD
  //
  return foo
    ? foo + 1 :
    bar;
```

``` js
  //
  // BAD
  //
  return foo
    ? function (wtf) {
      return foo + 1; // No multi-line return values!
    }
    : bar;
```

<hr>

- **RULE**: Ternary operators combined with `return` **should be** preferred over `if (err) { return }` blocks.

``` js
  //
  // OK
  //
  if (err) {
    return callback(err);
  }

  callback();
```

``` js
  //
  // GOOD
  //
  return err
    ? callback(err)
    : callback();
```

**[[â¬†]](#table-of-contents)**

## Errors

- **RULE**: You **must always** throw or return an error. [A string is not an Error](http://www.devthought.com/2011/12/22/a-string-is-not-an-error/).

> If you want more descriptive Errors, use [errs](https://github.com/flatiron/errs).

``` js
//
// GOOD
//
throw new Error('I have a call-stack and other good things.');
```

``` js
//
// GOOD
//
callback(new Error('I have a call-stack and other good things.'));
```

``` js
//
// BAD
//
throw 'I have no call-stack no interesting properties.';
```

``` js
//
// BAD
//
callback('I have no call-stack no interesting properties.');
```

``` js
//
// BAD
//
throw { message: 'I have no call-stack no interesting properties.' };
```

``` js
//
// BAD
//
callback({
  message: 'I have no call-stack no interesting properties.'
});
```

**[[â¬†]](#table-of-contents)**

## Exports

- **RULE**: If you are exporting something, it **should** be exported on the same line as the declaration.

> Makes it easier to understand what the exports are immediately in the same context.

``` js
//
// GOOD
//
var Foo = exports.Foo = function () {
  //...
};
```

``` js
//
// BAD
//
var Foo = function () {
  //...
};

//
// Lots of other code changing my mental context
// by the time I see Foo again I forgot what it was.
//

exports.Foo = Foo;
```

**[[â¬†]](#table-of-contents)**

## Async Programming

- **RULE**: You **must not** use promises.
- **RULE**: You **must** use [async](https://github.com/caolan/async).

> Just use async. If you love promises then sorry; this decision
> is final and _not up for debate_ **_â€¦ ever._**

``` js
//
// GOOD
//
var async = require('async');
```

``` js
//
// BAD
//
var Q = require('q');
```

<hr>

- **RULE**: A given function **must not** have more than **three** callback functions.

> Rule of three. What? It works in fairy tales.

> INSERT CODE EXAMPLES HERE

- **RULE**: Named functions **should** be preferred over anonymous inline functions.

**[[â¬†]](#table-of-contents)**

### Attribution (with modifications and additions)

* https://github.com/cloudhead/styleguide/blob/master/JavaScript.md
* https://github.com/airbnb/javascript
