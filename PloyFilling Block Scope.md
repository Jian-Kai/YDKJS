# 🌜  PloyFiling Block Scople 🌛 #

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

## [Traceur](http://google.github.io/traceur-compiler/demo/repl.html#) ##

>Transpiling ES6 features into pre-ES6 (mostly ES5, but not all!) for general usage.

## Implicit vs. Explicit Blocks ##

- `let block`

        { let a = 2;
            console.log( a );
        }

        console.log( a ); // ReferenceError
- `let statement`

        let (a = 2) {
            console.log( a ); // 2
        }

        console.log( a ); // ReferenceError
