<div align="center">

# Learn `TypeScript`

Learn `TypeScript` 
to enhance your `JavaScript` skills 
with **_type_ safety**. 

[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/dwyl/learn-typescript/ci.yml?label=build&style=flat-square&branch=main)](https://github.com/dwyl/learn-typescript/actions/workflows/ci.yml)
[![codecov.io](https://img.shields.io/codecov/c/github/dwyl/learn-typescript/master.svg?style=flat-square)](https://codecov.io/github/dwyl/learn-typescript?branch=master)
[![TypeScript Version](http://img.shields.io/badge/TypeScript-v5-brightgreen.svg?style=flat-square "Latest Typescript")](https://www.typescriptlang.org/download/)
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat-square)](https://github.com/dwyl/learn-typescript/issues)
[![HitCount](https://hits.dwyl.com/dwyl/learn-typescript.svg)](https://hits.dwyl.com/dwyl/learn-typescript)

</div>

# Why? 🤷‍♀️

You are working on -
or planning to work on - 
a large-scale `JavaScript` project
and don't want the pain of 
`"Uncaught TypeError: undefined is not a function"` ... 😢

# Who? 👥

Any software engineer
with (or without) 
`JavaScript` skills
who wants a better experience. 😍


# What? 💭

`TypeScript` is a 
[superset](https://en.wikipedia.org/wiki/Subset)
of `JavaScript`: 

<img src="https://github.com/dwyl/learn-typescript/assets/194400/f66be0cf-6689-4998-a312-fe83031c76bc" 
    width="300" alt="TypeScript superset of JavaScript">

This means it _includes_ all the 
[features](https://github.com/dwyl/Javascript-the-Good-Parts-notes)
we know and love/hate
from `JavaScript`
and has many _additional_ 
features, `types` and tooling
to make our lives easier.

`JavaScript` is 
[**_dynamically_ typed**](https://en.wikipedia.org/wiki/Dynamic_programming_language)
which means
variables can be assigned _any_ value 
by the interpreter at runtime 
based on the variable's value at the time.

This is great if you need flexibility while building something _fast_,
but it becomes a problem later when your function needs to _know_ 
what type of variable it is going to receive. 

## Quick _Example_! 1️⃣ + 2️⃣

The advantage of **_static_ types** 
is best illustrated by a _quick example_,
a simple addition function in `JavaScript`:

```js
function add (x, y) {
  return x + y;
}
```

If we invoke the `add` function with two numbers:

```js
add(1, 2)
> 3
```

So far so good.
And if we accidentally `add` a `number` to a `string`:

```js
add(1, "hello")
> '1hello'
```

It **_still_ works** because `JavaScript` has type-coerced the `1` to a `string`
and returned a `string`, in this case `'1hello'` as the result! 

What if somehow a 
[`NaN`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)
value gets passed into the function?

```js
add(1, NaN)
> NaN
```

Well now the `NaN` cascades through the rest of your Application without being caught!
If you're building an interface for anything in ***Finance***,
the _last_ thing you want is a `NaN` value sneaking in
as the result of a simple calculation. 

We could add a bunch of "checking" code 
to our simple `add` function 
to "guard" against non-numeric values:

```js
function add (x, y) {
  if(isNaN(x) || isNaN(y)) {
    throw new Error(`Arguments to add function ${x} or ${y} are non-numeric!`);
  }
  return x + y;
}
```
Adding this kind of code _works_,
but it has to be **_unit_ tested**.

> **Note**: If you're totally new to **Test-Driven Development**,
consider trying our
[`learn-tdd`](https://github.com/dwyl/learn-tdd)
tutorial. 

Even a basic function like `add`
ends up being a _lot_ more lines
of code and tests ...

`TypeScript` prevents this and 
_many_ other bugs from entering your codebase
by simply _typing_ the arguments for the function!

```ts
function add(x: number, y: number): number {
  return x + y;
}
```

Here we have clearly defined the `type` 
of the arguments to be `number` 
and the `return` is also a `number`.
If we attempt to invoke the `add` function
with a `string` (or any other non-numeric value):

```ts
add(1, "hello")
```

the `TypeScript` compiler will 
throw a _compile_ time error:

```ts
Argument of type 'string' is not assignable to parameter of type 'number'.
```

Try it for yourself on
the `TypeScript` _playground_:
[typescriptlang.org/play](https://www.typescriptlang.org/play/?#code/GYVwdgxgLglg9mABAQwCaoBQA8BciwgC2ARgKYBOANIgJ54EkUCU9RZ5iA3gFCKLmkoIckiyIA1LQDc3AL7duaTAEZqAIgAWpADba4apgqA)


![typescript-error-string-not-number](https://github.com/dwyl/learn-nextjs/assets/194400/c0dc988b-9866-47ae-acc8-4b3c9f9642bf)

You can use the playground to learn the basics online without installing anything,
but if you want to get serious about _building_ something, 
you'll need to _install_ `TypeScript` on your machine. 


# How? 👩‍💻

Buckle up! You're in for a ride! 🎢

## Install

Install and save `typescript`
as a `devDependency`:

```sh
npm install typescript tsx --save-dev
```

## Quick Example

Create a file called `add.ts`
and add the following lines of code to it:

```ts
export function add(x: number, y: number): number {
  return x + y;
}

console.log(add(1, 2))
```

Once saved, run the the file with the command:

```sh
npx tsx add.ts
```

You should see the output:
```sh
3
```

So we know the file compiles and `add` function _works_.

### _Test_ `add` Function

Create a new file called `add.test.ts`
and type (or paste) the following code:

```ts
import tap, { Test } from 'tap';
import { add } from './add.ts';

tap.test('add two numbers', (t: Test) => {
  t.equal(add(1, 2), 3);
  t.end();
})

tap.test('add a negative number should work', (t: Test) => {
  t.equal(add(1, -2), -1);
  t.end();
})
```

This file just imports the `tap` file 


### Setup the Testing Library & Scripts

Download the testing library and save to `package.json`:

```sh
npm install tap @tapjs/typescript nyc --save-dev
```

This will install the following 3 packages:

- `tap` - simple testing library
  [node-tap.org](https://node-tap.org/)
- `@tapjs/typescript` - tap `TypeScript` plugin
  https://tapjs.github.io/tapjs/modules/_tapjs_typescript.html
- `nyc` - test/code coverage library 
  https://github.com/istanbuljs/nyc

You don't need to know how any of these work,
but if you're curious you can follow the links and read.

With those `devDependencies` installed, 
open your `package.json` file and add the following `scripts` definition:

```json
"scripts": {
  "test": "nyc tap ./add.test.ts",
  "coverage": "nyc --report html tap ./add.test.ts && open coverage/index.html"
},
```

Once you have _saved_ the `package.json` file. 
You can _run_ the tests using the command:

```sh
npm test
```

You should see output similar to the following:

```sh
> nyc tap ./add.test.ts

 PASS  add.test.ts 2 OK 773ms


  🌈 TEST COMPLETE 🌈


Asserts:  2 pass  0 fail  2 of 2 complete
Suites:   1 pass  0 fail  1 of 1 complete

# { total: 2, pass: 2 }
# time=823.167ms


=============================== Coverage summary ===============================
Statements   : 100% ( 2/2 )
Branches     : 100% ( 0/0 )
Functions    : 100% ( 1/1 )
Lines        : 100% ( 2/2 )
================================================================================
```

`#success`



Instead of duplicating content here, 
please see:
[typescriptlang.org/docs/handbook](https://www.typescriptlang.org/docs/handbook/)

> **Note**: we will be extending this doc 
> as needed, but until then, we recommend the _official_ docs!

<!--
## Types
-->



## Relevant Reading & Useful Links

- Home: 
[typescriptlang.org](https://www.typescriptlang.org/)
- What is `TypeScript` and Why You Should Use It For Your _Next_ Project?
https://prismic.io/blog/what-is-typescript
- What problem does `TypeScript` _solve_?
https://dev.to/ricardopaul/what-problem-does-typescript-solve-5fka
- Getting started with `TypeScript`:
https://dev.to/newswim/getting-started-with-typescript-25l9
- How to run `TypeScript` files from command line?
https://stackoverflow.com/questions/33535879/how-to-run-typescript-files-from-command-line