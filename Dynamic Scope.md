# 🌜  Dynamic Scope 🌛 #

## Dynamic Scope v.s. Lexical Scope

> `Dynamic Scope` actually is a near cousin to another mechanism [` this `](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/this) in JavaScript .

###Here is an example of Dynamic Scope :###

    function foo() {
        console.log( a ); // What will console.log be?
    }

    function bar() {
        var a = 3;
        foo();
    }

    var a = 2;

    bar();

> the scope chain is based on the `call-stack`, not the nesting of scopes in code.

###Scope Chain :###

    function foo() { -----(find foo (3))
        console.log( a );  -----(call a (4))
    }

    function bar() {  -----(find bar (1))
        var a = 3; -----(find a (5))
        foo(); -----(call foo (2))
    }

    var a = 2;

    bar();  -----(call bar (0))

### How about Lexical Scope : ###

    function foo() {
        console.log( a ); // What will console.log be?
    }

    function bar() {
        var a = 3;
        foo();
    }

    var a = 2;

    bar();
> `RHS reference` to a in foo() will be resolved to the global variable a , which will result in value 2 being output