# 🌜  PloyFilling Block Scople 🌛 #

## Use block scope in pre-ES6 environments ##

> `let` and `const` are `Block Scople`.

- ES6

        {
            let a = 2;
            console.log( a ); // 2
        }
        console.log( a ); // ReferenceError

- ES3

        try{throw 2}
        catch(a){
            console.log(a); // 2
        }
        console.log(a); // ReferenceError

>The `catch` clause has block-scoping to it, which means it can be used as a polyfill for block scope in pre-ES6 environments.

## Other PloyFiling Example ##

- ES6 Default Parameters

        function sayHi(name = 'Jack') {
            return name;
        }

        sayHi(); // "Jack"
        sayHi(undefined); // "Jack"
        sayHi('Apple'); // "Apple"

- ES6 Default Parameters in ES5

        function sayHi() {
            var name = arguments.length <= 0 || arguments[0] === undefined ? 'Jack' : arguments[0];

            return name;
        }

        sayHi(); // "Jack"
        sayHi(undefined); // "Jack"
        sayHi('Apple'); // "Apple"

## [Traceur](http://google.github.io/traceur-compiler/demo/repl.html#) ##

>Transpiling ES6 features into pre-ES6 (mostly ES5, but not all!) for general usage.

## Implicit vs. Explicit Blocks ##

- `Implicit Block`
> Mplicitly hijacking an existing block

        { 
            let a = 2;
            console.log( a );
        }

        console.log( a ); // ReferenceError

- `Explicit Block`
> Creates an explicit block for its scope binding

        let (a = 2) {
            console.log( a ); // 2
        }

        console.log( a ); // ReferenceError


> But The `let-statement` form is not included in ES6.

## [let-er](https://github.com/getify/let-er) ##

> A `build-step` code transpiler, but its only task is to find `let-statement` forms and transpile them.

> use let-er as the first ES6 transpiler step, and then pass your code through something like Traceur if necessary.

## Performance of `try/catch` ##

> why not just use an IIFE to create the scope?

- Firstly, the performance of try/catch is slower, but there's no reasonable assumption that it has to be that way, or even that it always will be that way. Since the official TC39-approved ES6 transpiler uses try/catch, the Traceur team has asked Chrome to improve the performance of try/catch, and they are obviously motivated to do so.

- Secondly, IIFE is not a fair apples-to-apples comparison with try/catch, because a function wrapped around any arbitrary code changes the meaning, inside of that code, of this, return, break, and continue. IIFE is not a suitable general substitute. It could only be used manually in certain cases.
