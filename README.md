# angular-tslint-rules [![npm version](https://badge.fury.io/js/angular-tslint-rules.svg)](https://www.npmjs.com/package/angular-tslint-rules) [![npm downloads](https://img.shields.io/npm/dm/angular-tslint-rules.svg)](https://www.npmjs.com/package/angular-tslint-rules)

Shared [TSLint] & [codelyzer] rules to enforce a consistent code style for [Angular] development

[![CircleCI](https://circleci.com/gh/ng-seed/angular-tslint-rules.svg?style=shield)](https://circleci.com/gh/ng-seed/angular-tslint-rules)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)
[![Greenkeeper badge](https://badges.greenkeeper.io/ng-seed/angular-tslint-rules.svg)](https://greenkeeper.io/)

> Please support this project by simply putting a Github star. Share this library with friends on Twitter and everywhere else you can.

The value of the software produced is directly affected by the **quality of the codebase**, and not every developer might
- be **aware of the potential pitfalls** of certain constructions in [TypeScript],
- be **introduced into certain conventions** when using the [Angular] framework,
- know that not every developer is as capable in **understanding an elegant** (*but abstract*) **solution** as the original
developer.

For that purpose, we need to use **static code analysis tools** such as [TSLint] and [codelyzer] to check readability, maintainability,
and functionality errors.

Although complying with these tools may seem to appear as **undesired overhead** or may **limit creativity**, it becomes
**easier** for any new developers to **read**, **preventing** a lot of **time/frustration spent** figuring out the structure
and characteristics of the code.

Containing a set of [TSLint] and [codelyzer] rules, **`angular-tslint-rules`** has been compiled using many contributions
from colleagues, commercial/open-source projects and some other sources from the Internet, as well as years of development
using the [Angular] framework.

If you have questions, comments or suggestions, just create an issue on this repository. I'll try to revise and republish
these rules with new insights, experiences and remarks in alignment with the updates on [TSLint] and [codelyzer].

**Note**: The following set of rules depend on:
- [TSLint] v5.12.0
- [codelyzer] v4.5.0

## Table of contents:
- [Getting started](#getting-started)
  - [Installation](#installation)
- [Usage](#usage)
- [Rules](#rules)
  - [Class and Member design](#class-and-member-design)
  - [Interface design](#interface-design)
  - [Function design](#function-design)
    - [Anonymous functions](#anonymous-functions)
    - [Async functions](#async-functions)
  - [Variable design](#variable-design)
  - [Requires and Imports](#requires-and-imports)
  - [Types](#types)
  - [Objects](#objects)
  - [Strings](#strings)
  - [Operators](#operators)
  - [Conditional statements](#conditional-statements)
  - [`for` statement](#for-statement)
  - [`switch` statement](#switch-statement)
  - [`try` statement](#try-statement)
  - [Maintainability](#maintainability)
  - [Layout](#layout)
    - [Curly braces](#curly-braces)
    - [Whitespace](#whitespace)
    - [Empty lines](#empty-lines)
    - [Alignment](#alignment)
  - [Naming](#naming)
    - [Files](#files)
    - [Classes and Interfaces](#classes-and-interfaces)
    - [Variables and Functions](#variables-and-functions)
  - [Documentation](#documentation)
    - [Inline Comments](#inline-comments)
    - [JSDoc Comments](#jsdoc-comments)
  - [Misc](#misc)
  - [Codelyzer rules](#codelyzer-rules)
- [Contributing](#contributing)
- [License](#license)

## <a name="getting-started"></a> Getting started
### <a name="installation"></a> Installation
You can install **`angular-tslint-rules`** using `npm`
```
npm install angular-tslint-rules --save
```

**Note**: You should have already installed [TSLint] and [codelyzer].

## <a name="usage"></a> Usage
To use these [TSLint] rules, use **configuration inheritance** via the **`extends`** keyword.

A sample configuration is shown below, where `tslint.json` lives adjacent to your `node_modules` folder:
```json
{
  "rulesDirectory": [
    "node_modules/codelyzer"
  ],
  "extends": ["angular-tslint-rules"],
  "rules": {
    // override tslint rules here
    ...
  }
}
```

## <a name="rules"></a> Rules
### <a name="class-and-member-design"></a> Class and Member design
- *Do not use* **classes** unless required.
```json
"no-unnecessary-class": [
  true,
  "allow-constructor-only",
  "allow-static-only",
  "allow-empty-class"
]
```

- *Do not specify* the **`public`** keyword (*this is the default accessibility level*).
- **`private`** and **`private static`** members in classes should be **denoted** with the **`private`** keyword.
```json
"member-access": [
  true,
  "no-public"
]
```

- Member ordering should be in the following way:
  - **Public members** should be ordered **before private members**.
  - **Static members** should be ordered **before instance members**.
  - **Variables** should be ordered **before functions**.
```json
"member-ordering": [
  true,
  "public-before-private",
  "static-before-instance",
  "variables-before-functions"
]
```

- *Always prefer* **readonly** private members (*maintain immutability*).
```json
"prefer-readonly": true
```

- Member **overloads** should be **consecutive**.
```json
"adjacent-overload-signatures": true
```

- *Always prefer* **unifying any two overloads** into one, by using a **union** or an **optional/rest parameter**. 
```json
"unified-signatures": true
```

- *Always prefer* functions over **`private`** members that do not use **`this`**.
```json
"prefer-function-over-method": [
  true,
  "allow-public",
  "allow-protected"
]
```

- *Do not use* a **class method** *outside* of a **method call**.
```json
"no-unbound-method": [true, "ignore-static"]
```

- *Do not use* the **`this`** keyword **outside class context** (*including functions in methods*).
```json
"no-invalid-this": [
  true,
  "check-function-in-method"
]
```

- *Do not assign* **`this`** to local **variables**.
```json
"no-this-assignment": true
```

- *Do not use* blank **constructors**.
```json
"unnecessary-constructor": true
```

- *Do not invoke* the **`super`** method **twice** in a constructor (*except in branched statements or nested class constructors*).
```json
"no-duplicate-super": true
```

- *Always prefer* parentheses **`()`** when invoking a **constructor** via the **new** keyword.
```json
"new-parens": true
```

- *Do not define* **`new`** for **classes**.
```json
"no-misused-new": true
```

- *Do not use* the **constructors** of **`String`**, **`Number`**, and **`Boolean`**.
```json
"no-construct": true
```

### <a name="interface-design"></a> Interface design
- *Do not define* **constructors** for **interfaces**.
> See: [Class and Member design](#class-and-member-design)

- *Do not use* **empty interfaces**.
```json
"no-empty-interface": true
```

- *Always prefer* **`foo(): void`** over **`foo: () => void`** in **interfaces** and **types**.
```json
"prefer-method-signature": true
```

- *Always prefer* an **interface declaration** over a **type literal** (**`type T = { ... }`**).
```json
"interface-over-type-literal": true
```

### <a name="function-design"></a> Function design
- **Functions** should be defined right **after** the **variable declarations**.
> See: [Class and Member design](#class-and-member-design)

- *Do not use* the *built-in* **function constructor**.
```json
"function-constructor": true
```

- *Do not reassign* function **parameters** (*maintain immutability*).
```json
"no-parameter-reassignment": true
```

- *Do not use* **void expressions** in **statement** position.
```json
"no-void-expression": true
```

- *Always prefer* **`return;`** in **void** functions and **`return undefined;`** in **value-returning** functions.
```json
"return-undefined": true
```

- *Do not invoke* **`arguments.callee`** within a function, as it makes **impossible** various **performance optimizations**.
```json
"no-arg": true
```

#### <a name="anonymous-functions"></a> Anonymous functions
- *Always prefer* defining anonymous functions as **fat-arrow/lambda** `() => { }` functions.
```json
"only-arrow-functions": true
```

- **fat-arrow/lambda** functions should have parenthesis **`()`** around the **function parameters** (*except if removing
them is allowed by TypeScript*).
```json
"arrow-parens": [
  true,
  "ban-single-arg-parens"
]
```

- *Always prefer* **`() => x`** over **`() => { return x; }`**.
```json
"arrow-return-shorthand": [
  true,
  "multiline"
]
```

- *Always prefer* just **`f`** over **`x => f(x)`**.
```json
"no-unnecessary-callback-wrapper": true
```

- *Do not use* unnecessary and/or misleading **scope bindings** on functions.
```json
"unnecessary-bind": true
```

#### <a name="async-functions"></a> Async functions
- *Always prefer* marking **`async`** functions returning a **`Promise`**.
```json
"promise-function-async": true
```

- *Do not use* the **unnecessary** **`async`** (*if the awaited value that is not a `Promise`*).
```json
"await-promise": true
```

- *Do not use* the **unnecessary** **`return await`**.
```json
"no-return-await": true
```

- *Do not use* **floating** **`Promise`**.
```json
"no-floating-promises": true
```

### <a name="variable-design"></a> Variable design
- *Do not use* a **variable** before declaring.
```json
"no-use-before-declare": true
```

- *Always prefer* **`const`** keyword **where appropriate**, for values that should never change.
- *Avoid using* **`let`** (*maintain immutability*).
```json
"prefer-const": true
```

- *Do not use* the **`var`** keyword.
```json
"no-var-keyword": true
```

- *Do not use* **implied global variables**.
- *Do not define* a variable on the **global scope** from within a **smaller scope**.
```json
"no-shadowed-variable": [
  true,
  {
    "temporalDeadZone": false
  }
]
```

- Declare **one variable** at a time (*except in loops*).
```json
"one-variable-per-declaration": [
  true,
  "ignore-for-loop"
]
```

- *Do not use* **duplicate variable names** in the same block scope.
```json
"no-duplicate-variable": [
  true,
  "check-parameters"
]
```

- *Do not use* a **`var`**/**`let`** statement or destructuring initializer to be **initialized** to **`undefined`**. 
```json
"no-unnecessary-initializer": true
```

### <a name="requires-and-imports"></a> Requires and Imports
- *Do not **import*** modules that are *not listed* as a **dependency** in the project's **`package.json`**.
```json
"no-implicit-dependencies": true
```

- *Do not use* **`import`** statements with **side-effect**.
```json
"no-import-side-effect": [
  true,
  {
    "ignore-module": "(hammerjs|core-js|zone.js)"
  }
]
```

- *Always use* the **`import`** statement keywords in **alphabetical order**.
```json
"ordered-imports": [
  true,
  {
    "import-sources-order": "case-insensitive",
    "named-imports-order": "case-insensitive",
    "grouped-imports": true
  }
]
```

- *Always use* a **single** **`import`** statement per module.
```json
"no-duplicate-imports": true
```

- *Do not use* **`require`** statements at all (*use **ES6-style** **`import`** statement instead*).
```json
"no-require-imports": true
```

- *Do not use* **default imports** and **exports** in ES6-style modules.
```json
"no-default-import": true,
"no-default-export": true
```

- *Do not use* **`/// <reference path=> imports`** statements at all (*use **ES6-style** **`import`** statement instead*).
```json
"no-reference": true
```

### <a name="types"></a> Types
- *Always prefer* defining the **return type** of functions, methods and property declarations **explicitly**.
- Types should be used **whenever necessary** (*no implicit **`any`***).
```json
"typedef": [
  true,
  "call-signature",
  "property-declaration"
]
```

- *Always prefer* **type inference** over **explicit type declaration** (*except for function return types*).
```json
"no-inferrable-types": true
```

- *Do not use* **type inference** of `{}` (*empty object type*).
```json
"no-inferred-empty-object-type": true
```

- *Do not use* the **default** type arguments **explicitly**.
```json
"use-default-type-parameter": true
```

- Meanwhile, *avoid* **type assertion** for **object literals**.
```json
"no-object-literal-type-assertion": true
```

- *Always prefer* the use of **`as Type`** for type assertions over **`<Type>`**.
```json
"no-angle-bracket-type-assertion": true
```

- *Do not use* **unnecessary** type assertions.
```json
"no-unnecessary-type-assertion": true
```

- *Always prefer* writing an **interface** or **literal type** with just a **call signature** as a function type.
```json
"callable-types": true
```

- *Do not use* the **`null`** keyword, always return **`undefined`** instead of a **`null`** reference.
```json
"no-null-keyword": true
```

- *Do not use* **non-null** assertions.
```json
"no-non-null-assertion": true
```

- **Arrays** should be defined as **`Array<type>`** instead of **`type[]`**.
```json
"array-type": [
  true,
  "generic"
]
```

### <a name="objects"></a> Objects
- *Always prefer* **ES6 object spread operator** whenever possible.
```json
"prefer-object-spread": true
```

- *Always prefer* **ES6 object literal shorthand** whenever possible.
```json
"object-literal-shorthand": true
```

- *Always prefer* object property names **using literals** whenever possible.
```json
"object-literal-key-quotes": [
  true,
  "as-needed"
]
```

- *Do not use* **string literal** property access.
```json
"no-string-literal": true
```

### <a name="strings"></a> Strings
- *Always prefer* single-quotes **`''`** for all strings, and use double-quotes **`""`** for strings within strings.
```json
"quotemark": [
  true,
  "single",
  "avoid-template",
  "avoid-escape"
]
```

- *Always prefer* **template expressions** over string **literal concatenation**.
```json
"prefer-template": true
```

- *Do not use* string templates outside **template strings** (**``**).
```json
"no-invalid-template-strings": true
```

### <a name="operators"></a> Operators
- *Always prefer* using **`===`** and **`!==`** operators whenever possible.
> **`==`** and **`!=`** operators do type coercion, which can lead to **headaches** when debugging code.
```json
"triple-equals": [
  true,
  "allow-null-check"
]
```

- *Always prefer* explicit **`+= 1`** and **`-= 1`** *pre-unary* **operators** over **`++i`** and **`--i`**.
```json
"increment-decrement": [
  true,
  "allow-post"
]
```

- *Always prefer* using **operands** of the **same type** with the **`+``** **operator**.
```json
"restrict-plus-operands": true
```

- In a binary expression, a **literal** should always be on the **right-hand side**.
```json
"binary-expression-operand-order": true
```

- *Do not use* the **`delete`** operator with dynamic key expressions.
```json
"no-dynamic-delete": true
```

- *Do not use* **bitwise** operators.
```json
"no-bitwise": true
```

- *Always prefer* using **`isNan`** function to check **`NaN`** references.
```json
"use-isnan": true
```

- Assignment expressions inside of the condition block of **`if`**, **`while`**, and **`do while`** statements should be
**avoided**.
```json
"no-conditional-assignment": true
```

### <a name="conditional-statements"></a> Conditional statements
- *Always prefer* **conditional expression** over a standard **`if`** statement.
```json
"prefer-conditional-expression": [
  true,
  "check-else-if"
]
```

- *Do not* **compare** to a **boolean literal** (*ex: `x === true`*).
```json
"no-boolean-literal-compare": true
```

- *Do not use* any *always* **truthy**/**falsy** condition in **boolean expressions** (*ex: `val || undefined`*). 
```json
"strict-boolean-expressions": [
  true,
  "allow-undefined-union",
  "allow-string",
  "allow-enum",
  "allow-number",
  "allow-mix"
]
```

### <a name="for-statement"></a> `for` statement
- *Always prefer* **`while`** loop over a standard **`for`** loop *without* **initializer**, **incrementor** and/or **termination condition**.
```json
"prefer-while": true
```

- *Always prefer* **`for-of`** loop over a standard **`for`** loop.
```json
"prefer-for-of": true
```

- Filter **`for-in`** statements with an **`if`** statement (*this prevents accidental iteration over properties inherited
from an object???s prototype*).
```json
"forin": true
```

- *Do not* **iterate** over an **array** with a **`for-in`** loop.
```json
"no-for-in-array": true
```

### <a name="switch-statement"></a> `switch` statement
- Each **switch** statement should have a **default case**.
```json
"switch-default": true
```

- Each switch case **except default** should **end** with **`break`**, **`return`**, or **`throw`**.
```json
"no-switch-case-fall-through": true
```

- *Do not use* **duplicate** switch cases.
```json
"no-duplicate-switch-case": true
```

### <a name="try-statement"></a> `try` statement
- *Do not use* **control flow** statements, such as **`return`**, **`continue`**, **`break`** and **`throws`** in **`finally`**
blocks.
```json
"no-unsafe-finally": true
```

### <a name="maintainability"></a> Maintainability
- *Use* **UTF-8** encoding.
```json
"encoding": true
```

- *Limit* the **level of complexity** (cyclomatic complexity) in a function/method by **20 branches**.
```json
"cyclomatic-complexity": [
  true,
  20
]
```

- Files should not exceed **1500 lines** of code.
```json
"max-file-line-count": [true, 1500]
```

- Keep the length of **each line** under **140 characters**.
```json
"max-line-length": [
  true,
  140
]
```

- *Use* **2 spaces** for indentation.
```json
"indent": [
  true,
  "spaces",
  2
]
```

- All files should end in a **new line**.
```json
"eofline": true
```

### <a name="layout"></a> Layout
#### <a name="curly-braces"></a> Curly braces
*Use* **curly braces** as needed.
```json
"curly": [
  true,
  "as-needed"
]
```

#### <a name="whitespace"></a> Whitespace
Whitespaces should be used in the following circumstances:
- All branching statements (**`if`**/**`else`**/**`for`**/**`while`**) should be followed by **one space**.
- Variable declarations should be separated by **one space** around the **type specification** and **equals token**.
- There should be **one space** between the **typecast** and its **target**.
- All **operators** except the period **`.`**, left parenthesis **`(`**, and left bracket **`[`** should be separated from
their operands by **one space**.
- There should be **no space** between the **unary/incremental operators** **`!x, -x, +x, ~x, ++x, --x`** and its
**operand**.
- There should be **one space** between the **type operators** **`|`, `&`** and its **operand**. 
- There should be **one space** after the left curly brace **`{`** and before the right curly brace **`}`** containing **`import`**
statement keywords. 
- Each separator (**`,`**,**`;`**) in the control part of a **`for`** statement should be followed with **one space**.
- There should be **no space** after the **rest/spread operator** **`...`**.
- The left curly brace **`{`** followed by a right parenthesis **`)`** should always separated by **one space**.
```json
"whitespace": [
  true,
  "check-branch",
  "check-decl",
  "check-operator",
  "check-module",
  "check-separator",
  "check-rest-spread",
  "check-type",
  "check-typecast",
  "check-type-operator",
  "check-preblock"
]
```

- For each **call signature**, **index signature**, **parameter**, **property declaration** and **variable declaration**;
  - There should be **no space** between the **parameter** and the colon **`:`** indicating the **type declaration**.
  - There should be **one space** between the colon **`:`** and the **type declaration**.
```json
"typedef-whitespace": [
  true,
  {
    "call-signature": "nospace",
    "index-signature": "nospace",
    "parameter": "nospace",
    "property-declaration": "nospace",
    "variable-declaration": "nospace"
  },
  {
    "call-signature": "onespace",
    "index-signature": "onespace",
    "parameter": "onespace",
    "property-declaration": "onespace",
    "variable-declaration": "onespace"
  }
]
```

- For each **function**, **class member** and **constructor**;
  - There should be **no space** between the **name of the function/member** and the left parenthesis **`(`** of its parameter
  list.
- For each **fat-arrow/lambda function**;
  - There should be **one space** between the right parenthesis **`)`** and the **`=>`**.
```json
"space-before-function-paren": [
  true,
  {
    "anonymous": "never",
    "named": "never",
    "asyncArrow": "always",
    "method": "never",
    "constructor": "never"
  }
]
```

- There should be **no space** *within* **parenthesis**.
```json
"space-within-parens": 0
```

- Put **one space** between the **`import`** statement keywords.
```json
"import-spacing": true
```

- *Do not use* **trailing whitespaces** at the end of a line 
```json
"no-trailing-whitespace": true
```

#### <a name="empty-lines"></a> Empty lines
Empty lines improve code readability by allowing the developer to logically group code blocks.
- There should be an **empty line** before the **return** statement.
```json
"newline-before-return": true
```

- There should be a **separate line** for each **chained** method call.
```json
"newline-per-chained-call": true
```

- For each **function**, **anonymous function**, **class member**, **constructor**, **`else`**, **`catch`** and **`finally`**
statements;
  - There should be **one space** between the right parenthesis **`)`** and the left curly **`{`** brace that begins the
  statement body.
- For each **fat-arrow/lambda function**;  
  - There should be **one space** between the **`=>`** and the left curly brace **`{`** that begins the statement body.
- **`else`** statements should **indented to align** with the line containing the closing brace for the **`if`** statement.
- **`catch`** and **`finally`** statements should **indented to align** with the line containing the closing brace for the
**`try`** statement.  
```json
"one-line": [
  true,
  "check-open-brace",
  "check-whitespace",
  "check-else",
  "check-catch",
  "check-finally"
]
```

- *Do not use* more than **one empty line** in a row.
```json
"no-consecutive-blank-lines": [
  true,
  1
]
```

#### <a name="alignment"></a> Alignment
- A **semicolon** should be placed at the **end** of every **simple statement** (*except at the end of bound class methods*).
```json
"semicolon": [
  true,
  "always",
  "strict-bound-class-methods"
]
```

- **Vertically align** elements, members, parameters and statements (*helps maintain a readable, consistent style in your codebase*).
```json
"align": [
  true,
  "elements",
  "members",
  "parameters",
  "statements"
]
```

- *Do not use* **trailing commas** in **array and object literals**, **destructuring assignments**, **function typings**,
**named imports/exports** and **function parameters**.
```json
"trailing-comma": [
  true,
  {
    "multiline": "never",
    "singleline": "never",
    "esSpecCompliant": true
  }
]
```

### <a name="naming"></a> Naming
#### <a name="files"></a> Files
- **Files** should be in **kebab-case**.
```json
"file-name-casing": [
  true,
  "kebab-case"
]
```

#### <a name="classes-and-interfaces"></a> Classes and Interfaces
- **Class** and **interface names** should be in **PascalCase**.
```json
"class-name": true
```

- **Interface names** should not have an **`I`** prefix.
```json
"interface-name": [
  true,
  "never-prefix"
]
```

#### <a name="variables-and-functions"></a> Variables and Functions
- All **variable**, and **function names** should be in **camelCase**.
- *Do not use* **trailing** underscore **`_`** characters.
```json
"variable-name": [
  true,
  "check-format",
  "allow-leading-underscore",
  "ban-keywords"
]
```

### <a name="documentation"></a> Documentation
- *Always prefer* **single-line** or **JSDoc** comments.
```json
"comment-type": [
  true,
  "singleline",
  "doc"
]
```

#### <a name="inline-comments"></a> Inline Comments
- *Always prefer* **`//`** for all **inline comments**.
- There should be **one space** before the comment.
```json
"comment-format": [
  true,
  "check-space"
]
```

#### <a name="jsdoc-comments"></a> JSDoc Comments
- [JSDoc] comments should start with **`/**`** and end with **`*/`**.
```json
"jsdoc-format": [
  true,
  "check-multiline-start"
]
```

- *Do not use* redundant [JSDoc] comments.
```json
"no-redundant-jsdoc": true
```

- *Do not use* the **`// @ts-ignore`** comments.
```json
"ban-ts-ignore": true
```

### <a name="misc"></a> Misc
- *Do not use* the **`console`** method (*such messages are considered to be for debugging purposes and therefore might
ship to the production environment*).
```json
"no-console": [
  true,
  "log",
  "debug",
  "info",
  "time",
  "timeEnd",
  "trace"
]
```

- *Do not use* the **`debugger`** statement (*this might cause the environment to stop execution and start up a debugger,
if not omitted on the production code*).
```json
"no-debugger": true
```

- *Do not use* the **`eval`** function (*using `eval` on untrusted code might open a program up to several different injection
attacks*).
```json
"no-eval": true
```

- *Do not throw* **plain strings** or **concatenations of strings** (*because only `Error`s produce proper stack traces*).
```json
"no-string-throw": true
```

- *Do not use* **namespaces** (*using `namespace {}` is outdated*).
```json
"no-namespace": true
```

- *Do not use* internal **modules** (*using `module {}` is outdated*).
```json
"no-internal-module": true
```

- *Always prefer* decimal literals **beginning** with **`0`** (*instead of `.`*).
- *Avoid* decimal literals **ending** with a trailing **`0`**.
```json
"number-literal-format": true
```

- *Always prefer* the **`radix`** parameter to be specified when calling **`parseInt`**.
```json
"radix": true
```

- *Do not leave* **unused expressions** in the code.
```json
"no-unused-expression": [
  true,
  "allow-fast-null-checks"
]
```

- *Do not use* empty blocks **`{}`** in the code.
```json
"no-empty": true
```

- *Do not use* **missing elements** in arrays.
```json
"no-sparse-arrays": true
```

- *Do not use* **comma operator**.
```json
"ban-comma-operator": true
```

### <a name="codelyzer-rules"></a> Codelyzer rules
```json
"banana-in-box": true,
"contextual-life-cycle": true,
"decorator-not-allowed": true,
"pipe-impure": true,
"templates-no-negated-async": true,
"trackBy-function": true,
"i18n": [
  true,
  "check-id",
  "check-text"
],
"no-attribute-parameter-decorator": true,
"no-forward-ref": true,
"no-input-rename": true,
"no-life-cycle-call": true,
"no-output-named-after-standard-event": true,
"no-output-on-prefix": true,
"no-output-rename": true,
"no-queries-parameter": true,
"no-template-call-expression": true,
"no-unused-css": true,
"prefer-inline-decorator": true,
"prefer-output-readonly": true,
"use-life-cycle-interface": true,
"use-pipe-decorator": true,
"use-pipe-transform-interface": true,
"use-view-encapsulation": true,
"angular-whitespace": [
  true,
  "check-interpolation",
  "check-semicolon"
],
"component-class-suffix": [
  true,
  "Component"
],
"component-selector": [
  true,
  "element",
  [
    "ngx",
    "test"
  ],
  "kebab-case"
],
"directive-class-suffix": [
  true,
  "Directive"
],
"directive-selector": [
  true,
  "attribute",
  [
    "ngx",
    "test"
  ],
  "camelCase"
],
"import-destructuring-spacing": true,
"use-host-property-decorator": true,
"use-input-property-decorator": true,
"use-output-property-decorator": true
```

## <a name="contributing"></a> Contributing
If you want to file a bug, contribute some code, or improve documentation, please read up on the following contribution guidelines:
- [Issue guidelines](CONTRIBUTING.md#submit)
- [Contributing guidelines](CONTRIBUTING.md)
- [Coding rules](CONTRIBUTING.md#rules)
- [ChangeLog](CHANGELOG.md)

#### Thanks to
- [JetBrains], for their support to this open source project with free [WebStorm] licenses.

## <a name="license"></a> License
The MIT License (MIT)

Copyright (c) 2018 [Burak Tasci]

[TSLint]: https://github.com/palantir/tslint
[codelyzer]: https://github.com/mgechev/codelyzer
[Angular]: https://angular.io
[TypeScript]: https://github.com/Microsoft/TypeScript
[JSDoc]: http://usejsdoc.org
[JetBrains]: https://www.jetbrains.com/community/opensource
[WebStorm]:   https://www.jetbrains.com/webstorm
[Burak Tasci]: https://github.com/fulls1z3
